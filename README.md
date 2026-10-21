# Google AI Studio Docs — End-to-End Crawler

> Last verified: 2026-10-21 — see `docs/_last_verified.json` (rewritten daily by GitHub Actions).

Crawls **https://ai.google.dev/** completely (sitemap + linked reference domains: aistudio, saif, discuss, developer.android, developer.chrome) and saves clean markdown docs. Three stacks: **Scrapling** → **Crawl4AI** → **ScrapeGraphAI** (local, no LLM key).

## Install

```bash
pip install -r requirements.txt
python -m playwright install chromium
```

## Run (resume-safe — re-run to resume)

```bash
python3 crawl_ai.py --max-pages 8000 --concurrency 15
python3 update_incremental.py --check-only   # new URLs only, never recrawls
python3 update_incremental.py
```

## Layout

```
crawl_ai.py  update_incremental.py  requirements.txt
guide_code/      # coder guide + coder_scrape.py / coder_update.py
ai-docs-crawl.service  boot.sh  cloud-init.yaml   # spot-VM boot resilience
docs/            # output: <area>/<path>.md + _meta/ + _index.jsonl + _manifest.json
```

## Notes

- Sitemap's 6,854 URLs collapse to ~653 canonical (`?hl=` locale variants deduped); `*.md.txt` entries fetched as raw text.
- Login-walled hosts recorded as failed, not silently dropped.
