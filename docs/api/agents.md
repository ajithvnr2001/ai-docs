---
url: https://ai.google.dev/api/agents/
title: Gemini Agents API \u00a0|\u00a0 Gemini API \u00a0|\u00a0 Google AI for Developers
method: scrapling+scrapegraph
fetched_at: 2026-10-15T19:15:52.310704+00:00
---

# Gemini Agents API  |  Gemini API  |  Google AI for Developers

> Source: https://ai.google.dev/api/agents/

Gemini 4 Argon is now available. [Try it out](https://aistudio.google.com/prompts/new_chat?model=gemini-4-argon). 

  * [ Home ](https://ai.google.dev/)
  * [ Gemini API ](https://ai.google.dev/gemini-api)
  * [ API reference ](https://ai.google.dev/api)



Send feedback 

#  Gemini Agents API

Agents are systems that leverage Gemini models, a set of tools, and reasoning capabilities to perform complex, multi-step tasks and achieve specific goals. Unlike a single model call, an agent can plan, execute a series of actions, interact with external systems, and synthesize information to fulfill a user's request.

[View as markdown](https://ai.google.dev/static/api/agents.md.txt) [View the OpenAPI Spec](https://ai.google.dev/static/api/interactions.openapi.json)

This API is in Beta. Endpoints are under `/v1beta/`.

## CreateAgent

post  https://generativelanguage.googleapis.com/v1beta/agents 

Creates a new Agent (Typed version for SDK).

  * Request body
  * Response



### Request body

The request body contains data with the following structure:

agent_config AntigravityAgentConfig (optional)

Configuration parameters for the agent.

Configuration for the Antigravity agent runtime. Provides server-side control over the agent's execution environment and tool configuration.

#### Fields

max_total_tokens string (optional)

Max total tokens for the agent run.

model string (optional)

The model to use for agent reasoning.

type object (optional)

No description provided.

Always set to `"antigravity"`.

base_agent string (optional)

The base agent to extend.

base_environment EnvironmentConfig or string (optional)

The environment configuration for the agent.

Configuration for a custom environment.

#### Fields

env object (optional)

Environment variables to set in the sandbox environment.

environment_id string (optional)

Optional. The environment ID for the interaction. If specified, the request will update the existing environment instead of creating a new one.

network EnvironmentNetworkEgressAllowlist or enum (string) (optional)

Network configuration for the environment.

Network egress configuration for the environment.

#### Fields

allowlist array (EgressRule) or enum (string) (optional)

List of allowed domains and their configurations. Set to `"disabled"` to block all network egress.

Possible values:

  * `disabled`

All network egress is blocked.




sources array (Source) (optional)

No description provided.

A source to be mounted into the environment.

#### Fields

content string (optional)

The inline content if `type` is `INLINE`.

encoding string (optional)

Optional encoding for inline content (e.g. `base64`).

source string (optional)

The source of the environment. For Cloud Storage, this is the Cloud Storage path. For GitHub, this is the GitHub path.

target string (optional)

Where the source should appear in the environment.

type enum (string) (optional)

No description provided.

Possible values:

  * `gcs`

A Cloud Storage bucket.

  * `inline`

Inline content.

  * `repository`

A generic repository. The protocol prefix in the source URL identifies the provider (e.g., github://, gcs://).

  * `skill_registry`

A skill resource from the Skill Registry Service. Skill: projects/{project}/locations/{location}/skills/{skill} SkillRevision: projects/{project}/locations/{location}/skills/{skill}/revisions/{revision} Support mounting all skills under a project: projects/{project}/locations/{location}/skills.




type object (optional)

No description provided.

Always set to `"remote"`.

description string (optional)

Agent description for developers to quickly read and understand.

id string (optional)

The unique identifier for the agent.

system_instruction string (optional)

System instruction for the agent.

tools array (AgentTool) (optional)

The tools available to the agent.

A tool that the agent can use.

#### Possible Types

CodeExecution

A tool that can be used by the model to execute code.

type object (required)

No description provided.

Always set to `"code_execution"`.

Function

A tool that can be used by the model.

description string (optional)

A description of the function.

name string (optional)

The name of the function.

parameters object (optional)

The JSON Schema for the function's parameters.

type object (required)

No description provided.

Always set to `"function"`.

GoogleSearch

A tool that can be used by the model to search Google.

search_types array (enum (string)) (optional)

The types of search grounding to enable.

Possible values:

  * `web_search`

Setting this field enables web search. Only text results are returned.

  * `image_search`

Setting this field enables image search. Image bytes are returned.

  * `enterprise_web_search`

Setting this field enables enterprise web search.




type object (required)

No description provided.

Always set to `"google_search"`.

McpServer

A MCPServer is a server that can be called by the model to perform actions.

allowed_tools array (AllowedTools) (optional)

The allowed tools.

The configuration for allowed tools.

#### Fields

mode enum (string) (optional)

The mode of the tool choice.

Possible values:

  * `auto`

Auto tool choice.

  * `any`

Any tool choice.

  * `none`

No tool choice.

  * `validated`

Validated tool choice.




tools array (string) (optional)

The names of the allowed tools.

headers object (optional)

Optional: Fields for authentication headers, timeouts, etc., if needed.

name string (optional)

The name of the MCPServer.

type object (required)

No description provided.

Always set to `"mcp_server"`.

url string (optional)

The full URL for the MCPServer endpoint. Example: "https://api.example.com/mcp"

UrlContext

A tool that can be used by the model to fetch URL context.

type object (required)

No description provided.

Always set to `"url_context"`.

### Response

If successful, the response body contains data with the following structure:

agent_config AntigravityAgentConfig (optional)

Configuration parameters for the agent.

Configuration for the Antigravity agent runtime. Provides server-side control over the agent's execution environment and tool configuration.

#### Fields

max_total_tokens string (optional)

Max total tokens for the agent run.

model string (optional)

The model to use for agent reasoning.

type object (optional)

No description provided.

Always set to `"antigravity"`.

base_agent string (optional)

The base agent to extend.

base_environment EnvironmentConfig or string (optional)

The environment configuration for the agent.

Configuration for a custom environment.

#### Fields

env object (optional)

Environment variables to set in the sandbox environment.

environment_id string (optional)

Optional. The environment ID for the interaction. If specified, the request will update the existing environment instead of creating a new one.

network EnvironmentNetworkEgressAllowlist or enum (string) (optional)

Network configuration for the environment.

Network egress configuration for the environment.

#### Fields

allowlist array (EgressRule) or enum (string) (optional)

List of allowed domains and their configurations. Set to `"disabled"` to block all network egress.

Possible values:

  * `disabled`

All network egress is blocked.




sources array (Source) (optional)

No description provided.

A source to be mounted into the environment.

#### Fields

content string (optional)

The inline content if `type` is `INLINE`.

encoding string (optional)

Optional encoding for inline content (e.g. `base64`).

source string (optional)

The source of the environment. For Cloud Storage, this is the Cloud Storage path. For GitHub, this is the GitHub path.

target string (optional)

Where the source should appear in the environment.

type enum (string) (optional)

No description provided.

Possible values:

  * `gcs`

A Cloud Storage bucket.

  * `inline`

Inline content.

  * `repository`

A generic repository. The protocol prefix in the source URL identifies the provider (e.g., github://, gcs://).

  * `skill_registry`

A skill resource from the Skill Registry Service. Skill: projects/{project}/locations/{location}/skills/{skill} SkillRevision: projects/{project}/locations/{location}/skills/{skill}/revisions/{revision} Support mounting all skills under a project: projects/{project}/locations/{location}/skills.




type object (optional)

No description provided.

Always set to `"remote"`.

description string (optional)

Agent description for developers to quickly read and understand.

id string (optional)

The unique identifier for the agent.

system_instruction string (optional)

System instruction for the agent.

tools array (AgentTool) (optional)

The tools available to the agent.

A tool that the agent can use.

#### Possible Types

CodeExecution

A tool that can be used by the model to execute code.

type object (required)

No description provided.

Always set to `"code_execution"`.

Function

A tool that can be used by the model.

description string (optional)

A description of the function.

name string (optional)

The name of the function.

parameters object (optional)

The JSON Schema for the function's parameters.

type object (required)

No description provided.

Always set to `"function"`.

GoogleSearch

A tool that can be used by the model to search Google.

search_types array (enum (string)) (optional)

The types of search grounding to enable.

Possible values:

  * `web_search`

Setting this field enables web search. Only text results are returned.

  * `image_search`

Setting this field enables image search. Image bytes are returned.

  * `enterprise_web_search`

Setting this field enables enterprise web search.




type object (required)

No description provided.

Always set to `"google_search"`.

McpServer

A MCPServer is a server that can be called by the model to perform actions.

allowed_tools array (AllowedTools) (optional)

The allowed tools.

The configuration for allowed tools.

#### Fields

mode enum (string) (optional)

The mode of the tool choice.

Possible values:

  * `auto`

Auto tool choice.

  * `any`

Any tool choice.

  * `none`

No tool choice.

  * `validated`

Validated tool choice.




tools array (string) (optional)

The names of the allowed tools.

headers object (optional)

Optional: Fields for authentication headers, timeouts, etc., if needed.

name string (optional)

The name of the MCPServer.

type object (required)

No description provided.

Always set to `"mcp_server"`.

url string (optional)

The full URL for the MCPServer endpoint. Example: "https://api.example.com/mcp"

UrlContext

A tool that can be used by the model to fetch URL context.

type object (required)

No description provided.

Always set to `"url_context"`.

### Create Agent

####  Example Response
    
    
    {
      "description": "A helpful research assistant.",
      "base_agent": "antigravity-preview-05-2026",
      "base_environment": "remote",
      "id": "research-assistant-abc123",
      "system_instruction": "You are a helpful research assistant.",
      "tools": [
        {
          "type": "google_search"
        }
      ]
    }

### Agent with Sources

####  Example Response
    
    
    {
      "base_agent": "antigravity-preview-05-2026",
      "base_environment": {
        "type": "remote",
        "sources": [
          {
            "type": "inline",
            "content": "Always use matplotlib for charts. Include a summary table in every report.",
            "target": ".agents/AGENTS.md"
          },
          {
            "type": "repository",
            "source": "https://github.com/my-org/analysis-templates",
            "target": "/workspace/templates"
          }
        ]
      },
      "id": "data-analyst-abc123",
      "system_instruction": "You are a data analyst. Always include visualizations and export results as PDF."
    }

### Agent Forked from Environment

####  Example Response
    
    
    {
      "base_agent": "antigravity-preview-05-2026",
      "base_environment": "env_abc123",
      "id": "my-data-analyst-abc123",
      "system_instruction": "You are a data analyst. Use the template at /workspace/template.py for all reports."
    }

## ListAgents

get  https://generativelanguage.googleapis.com/v1beta/agents 

Lists all Agents.

  * Path / Query parameters
  * Response



### Path / Query Parameters

page_size integer (optional)

No description provided.

page_token string (optional)

No description provided.

parent string (optional)

Required. The parent resource to list agents from. Format: `projects/{project}/locations/{location}`

### Response

If successful, the response body contains data with the following structure:

agents array (Agent) (optional)

The list of agents.

next_page_token string (optional)

A token to retrieve the next page of results.

### List Agents

####  Example Response
    
    
    {
      "agents": [
        {
          "description": "A helpful research assistant.",
          "base_agent": "antigravity-preview-05-2026",
          "id": "research-assistant-abc123",
          "system_instruction": "You are a helpful research assistant.",
          "tools": [
            {
              "type": "google_search"
            }
          ]
        }
      ]
    }

## GetAgent

get  https://generativelanguage.googleapis.com/v1beta/agents/{agentsId} 

Gets a specific Agent.

  * Path / Query parameters
  * Response



### Path / Query Parameters

agentsId string (required)

Required. The name of the agent to retrieve.

### Response

If successful, the response body contains data with the following structure:

agent_config AntigravityAgentConfig (optional)

Configuration parameters for the agent.

Configuration for the Antigravity agent runtime. Provides server-side control over the agent's execution environment and tool configuration.

#### Fields

max_total_tokens string (optional)

Max total tokens for the agent run.

model string (optional)

The model to use for agent reasoning.

type object (optional)

No description provided.

Always set to `"antigravity"`.

base_agent string (optional)

The base agent to extend.

base_environment EnvironmentConfig or string (optional)

The environment configuration for the agent.

Configuration for a custom environment.

#### Fields

env object (optional)

Environment variables to set in the sandbox environment.

environment_id string (optional)

Optional. The environment ID for the interaction. If specified, the request will update the existing environment instead of creating a new one.

network EnvironmentNetworkEgressAllowlist or enum (string) (optional)

Network configuration for the environment.

Network egress configuration for the environment.

#### Fields

allowlist array (EgressRule) or enum (string) (optional)

List of allowed domains and their configurations. Set to `"disabled"` to block all network egress.

Possible values:

  * `disabled`

All network egress is blocked.




sources array (Source) (optional)

No description provided.

A source to be mounted into the environment.

#### Fields

content string (optional)

The inline content if `type` is `INLINE`.

encoding string (optional)

Optional encoding for inline content (e.g. `base64`).

source string (optional)

The source of the environment. For Cloud Storage, this is the Cloud Storage path. For GitHub, this is the GitHub path.

target string (optional)

Where the source should appear in the environment.

type enum (string) (optional)

No description provided.

Possible values:

  * `gcs`

A Cloud Storage bucket.

  * `inline`

Inline content.

  * `repository`

A generic repository. The protocol prefix in the source URL identifies the provider (e.g., github://, gcs://).

  * `skill_registry`

A skill resource from the Skill Registry Service. Skill: projects/{project}/locations/{location}/skills/{skill} SkillRevision: projects/{project}/locations/{location}/skills/{skill}/revisions/{revision} Support mounting all skills under a project: projects/{project}/locations/{location}/skills.




type object (optional)

No description provided.

Always set to `"remote"`.

description string (optional)

Agent description for developers to quickly read and understand.

id string (optional)

The unique identifier for the agent.

system_instruction string (optional)

System instruction for the agent.

tools array (AgentTool) (optional)

The tools available to the agent.

A tool that the agent can use.

#### Possible Types

CodeExecution

A tool that can be used by the model to execute code.

type object (required)

No description provided.

Always set to `"code_execution"`.

Function

A tool that can be used by the model.

description string (optional)

A description of the function.

name string (optional)

The name of the function.

parameters object (optional)

The JSON Schema for the function's parameters.

type object (required)

No description provided.

Always set to `"function"`.

GoogleSearch

A tool that can be used by the model to search Google.

search_types array (enum (string)) (optional)

The types of search grounding to enable.

Possible values:

  * `web_search`

Setting this field enables web search. Only text results are returned.

  * `image_search`

Setting this field enables image search. Image bytes are returned.

  * `enterprise_web_search`

Setting this field enables enterprise web search.




type object (required)

No description provided.

Always set to `"google_search"`.

McpServer

A MCPServer is a server that can be called by the model to perform actions.

allowed_tools array (AllowedTools) (optional)

The allowed tools.

The configuration for allowed tools.

#### Fields

mode enum (string) (optional)

The mode of the tool choice.

Possible values:

  * `auto`

Auto tool choice.

  * `any`

Any tool choice.

  * `none`

No tool choice.

  * `validated`

Validated tool choice.




tools array (string) (optional)

The names of the allowed tools.

headers object (optional)

Optional: Fields for authentication headers, timeouts, etc., if needed.

name string (optional)

The name of the MCPServer.

type object (required)

No description provided.

Always set to `"mcp_server"`.

url string (optional)

The full URL for the MCPServer endpoint. Example: "https://api.example.com/mcp"

UrlContext

A tool that can be used by the model to fetch URL context.

type object (required)

No description provided.

Always set to `"url_context"`.

### Get Agent

####  Example Response
    
    
    {
      "created": "2025-11-26T12:25:15Z",
      "display_name": "My Research Agent",
      "id": "ag_abc123",
      "object": "agent",
      "system_instruction": "You are a helpful research assistant.",
      "tools": [
        {
          "type": "google_search"
        }
      ],
      "updated": "2025-11-26T12:25:15Z"
    }

## DeleteAgent

delete  https://generativelanguage.googleapis.com/v1beta/agents/{agentsId} 

Deletes an Agent.

  * Path / Query parameters
  * Response



### Path / Query Parameters

agentsId string (required)

Required. The name of the agent to delete.

### Response

If successful, the response is empty.

### Delete Agent

## Resources

### Agent

An agent definition for the CreateAgent API. This message is the target for annotation-parser-based JSON parsing. New format: { "id": "customer-sentinel", "base_agent": "", "system_instruction": "...", "base_environment": { "type": "remote", "sources": [...] }, "tools": [ {"type": "code_execution"} ] }

#### Fields

agent_config AntigravityAgentConfig (optional)

Configuration parameters for the agent.

Configuration for the Antigravity agent runtime. Provides server-side control over the agent's execution environment and tool configuration.

#### Fields

max_total_tokens string (optional)

Max total tokens for the agent run.

model string (optional)

The model to use for agent reasoning.

type object (optional)

No description provided.

Always set to `"antigravity"`.

base_agent string (optional)

The base agent to extend.

base_environment EnvironmentConfig or string (optional)

The environment configuration for the agent.

Configuration for a custom environment.

#### Fields

env object (optional)

Environment variables to set in the sandbox environment.

environment_id string (optional)

Optional. The environment ID for the interaction. If specified, the request will update the existing environment instead of creating a new one.

network EnvironmentNetworkEgressAllowlist or enum (string) (optional)

Network configuration for the environment.

Network egress configuration for the environment.

#### Fields

allowlist array (EgressRule) or enum (string) (optional)

List of allowed domains and their configurations. Set to `"disabled"` to block all network egress.

Possible values:

  * `disabled`

All network egress is blocked.




sources array (Source) (optional)

No description provided.

A source to be mounted into the environment.

#### Fields

content string (optional)

The inline content if `type` is `INLINE`.

encoding string (optional)

Optional encoding for inline content (e.g. `base64`).

source string (optional)

The source of the environment. For Cloud Storage, this is the Cloud Storage path. For GitHub, this is the GitHub path.

target string (optional)

Where the source should appear in the environment.

type enum (string) (optional)

No description provided.

Possible values:

  * `gcs`

A Cloud Storage bucket.

  * `inline`

Inline content.

  * `repository`

A generic repository. The protocol prefix in the source URL identifies the provider (e.g., github://, gcs://).

  * `skill_registry`

A skill resource from the Skill Registry Service. Skill: projects/{project}/locations/{location}/skills/{skill} SkillRevision: projects/{project}/locations/{location}/skills/{skill}/revisions/{revision} Support mounting all skills under a project: projects/{project}/locations/{location}/skills.




type object (optional)

No description provided.

Always set to `"remote"`.

description string (optional)

Agent description for developers to quickly read and understand.

id string (optional)

The unique identifier for the agent.

system_instruction string (optional)

System instruction for the agent.

tools array (AgentTool) (optional)

The tools available to the agent.

A tool that the agent can use.

#### Possible Types

CodeExecution

A tool that can be used by the model to execute code.

type object (required)

No description provided.

Always set to `"code_execution"`.

Function

A tool that can be used by the model.

description string (optional)

A description of the function.

name string (optional)

The name of the function.

parameters object (optional)

The JSON Schema for the function's parameters.

type object (required)

No description provided.

Always set to `"function"`.

GoogleSearch

A tool that can be used by the model to search Google.

search_types array (enum (string)) (optional)

The types of search grounding to enable.

Possible values:

  * `web_search`

Setting this field enables web search. Only text results are returned.

  * `image_search`

Setting this field enables image search. Image bytes are returned.

  * `enterprise_web_search`

Setting this field enables enterprise web search.




type object (required)

No description provided.

Always set to `"google_search"`.

McpServer

A MCPServer is a server that can be called by the model to perform actions.

allowed_tools array (AllowedTools) (optional)

The allowed tools.

The configuration for allowed tools.

#### Fields

mode enum (string) (optional)

The mode of the tool choice.

Possible values:

  * `auto`

Auto tool choice.

  * `any`

Any tool choice.

  * `none`

No tool choice.

  * `validated`

Validated tool choice.




tools array (string) (optional)

The names of the allowed tools.

headers object (optional)

Optional: Fields for authentication headers, timeouts, etc., if needed.

name string (optional)

The name of the MCPServer.

type object (required)

No description provided.

Always set to `"mcp_server"`.

url string (optional)

The full URL for the MCPServer endpoint. Example: "https://api.example.com/mcp"

UrlContext

A tool that can be used by the model to fetch URL context.

type object (required)

No description provided.

Always set to `"url_context"`.

Send feedback 

Except as otherwise noted, the content of this page is licensed under the [Creative Commons Attribution 4.0 License](https://creativecommons.org/licenses/by/4.0/), and code samples are licensed under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0). For details, see the [Google Developers Site Policies](https://developers.google.com/site-policies). Java is a registered trademark of Oracle and/or its affiliates.

Last updated 2026-10-13 UTC.

Need to tell us more?  [[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Missing the information I need","missingTheInformationINeed","thumb-down"],["Too complicated / too many steps","tooComplicatedTooManySteps","thumb-down"],["Out of date","outOfDate","thumb-down"],["Samples / code issue","samplesCodeIssue","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-10-13 UTC."],[],[]] 
