# GUIDE — ai.google.dev docs: full redo + incremental updates (end to end)

Written from the run that produced 5,780 markdown pages in 6 hosts. Follow top-to-bottom to **redo the crawl from zero**, or skip to §3 for daily updates.

## 0. Scope + architecture

Crawls **https://ai.google.dev/** (653 canonical sitemap URLs after locale dedupe, plus raw `.md.txt` API mirrors) and linked reference domains at depth ≤1: `aistudio.google.com`, `saif.google`, `discuss.ai.google.dev`, `developer.android.com`, `developer.chrome.com` → lands under `docs/_subdomains/<host>/`.

Pipeline (`crawl_ai.py::fetch_one`):
`Scrapling Fetcher.get(stealthy_headers)` → main-content extract → **ScrapeGraphAI** `convert_to_md` (local, no key) → thin-content fallback **Crawl4AI** headless → **httpx** last resort. URLs ending `.txt` are fetched raw (no rendering).

State: `crawl_state.json` (visited/failed), `docs/_index.jsonl`, `docs/_meta/*/*.json`, `docs/_manifest.json`, `crawl.log`.

## 1. Setup (fresh machine)

```bash
git clone https://github.com/ajithvnr2001/ai-docs   # or start bare with the scripts
pip install -r requirements.txt
python -m playwright install chromium
mkdir -p tools && for t in scrapegraph-ai crawl4AI scrapling; do ln -s /data/opencode/cloudflare/tools/$t tools/$t; done
```

scrapegraph-ai 1.36.0 ships stale `langchain.prompts` imports — use the patched clone (tools/) or `sed 's/langchain\.prompts/langchain_core.prompts/'` its `utils/convert_to_md.py`.

## 2. Full crawl redo

```bash
python3 crawl_ai.py --max-pages 8000 --concurrency 15
```

- Seeds = `https://ai.google.dev/sitemap.xml` → `sitemap_0_of_1.xml`, locale variants deduped by `normalize_url()`; `?hl=` dropped; binaries/`.json`/login-walled hosts skipped and recorded.
- Fully resumable — rerun the same command; visited set is skipped.
- Watch: `tail -f crawl.log`; final state: `[done] visited=N failed=M` + `_manifest.json`.

Expected: ~5,780 pages total (`ai.google.dev` + 5 subdomain hosts), ~90MB.

## 3. Daily incremental updates (GitHub Actions)

`.github/workflows/update-docs.yml` runs daily 04:00 UTC (a pin-stagger with cloudflare 02:00 and copilotkit 03:00):

1. checkout → install pinned deps → `python3 update_incremental.py --concurrency 10`
   - fetches live sitemap + `lastmod`
   - **new** = URLs not in `_index.jsonl` → crawled
   - **stale** = `lastmod` > our `fetched_at` → refreshed newest-first, capped at 100/run
   - writes daily stamp `docs/_last_verified.json`, updates `_manifest.json`, stamps "Last verified:" in both READMEs
2. If anything changed: commit `chore: daily docs update <date>` + push with **retry-with-rebase** (on stamp-file conflicts it keeps our fresh copy: `git checkout --ours -- docs/_last_verified.json docs/_manifest.json`).

Run manually anytime: **Actions → daily-docs-update → Run workflow** (workflow_dispatch). Locally:

```bash
python3 update_incremental.py --check-only
python3 update_incremental.py --concurrency 10
```

## 4. Verifying a healthy corpus

```bash
python3 update_incremental.py --check-only            # expect new=0 (or a handful that then get fetched)
find docs -name '*.md' | wc -l                        # ~5,780
python3 -c "import json;print(json.load(open('docs/_last_verified.json')))"
```

A green daily Action that says "no changes" most days = healthy. If `new` grows monotonically without commits, check the Actions log for the push-retry dance.

## 5. VM eviction recovery

- `ai-docs-crawl.service` (`Restart=on-failure`) + `boot.sh` + `cloud-init.yaml` — after a reboot the service starts and the crawl resumes; when the crawl is already done the service stays idle (on-failure, no loop).
- One-time per new VM: attach `cloud-init.yaml` as custom-data.

## 6. Gotchas (real ones we hit)

| Symptom | Fix |
|---|---|
| 9 sitemap `.txt` files saved as garbage md | raw-text branch in `fetch_one` (urls ending `.txt` → httpx plain fetch) — keep it. |
| `Restart=always` re-crawled a *finished* corpus on boot | now `Restart=on-failure`; only start the service when you want a (re)crawl. |
| llms.txt returns 404 despite sitemap advertising it | not all sites ship it; seeds fall back to sitemap only — fine. |
| Stamp-file rebase conflicts in Actions | handled by the `--ours` checkout of `_last_verified.json` + `_manifest.json`. |
| `developer.android.com` reference explosion (100k+ gradle pages) | kept `--max-pages 8000` cap + depth ≤1 on reference domains; raise if you want the full Android reference (be ready for a multi-day crawl). |
