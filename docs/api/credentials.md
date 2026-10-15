---
url: https://ai.google.dev/api/credentials/
title: Gemini Credentials API \u00a0|\u00a0 Gemini API \u00a0|\u00a0 Google AI for Developers
method: scrapling+scrapegraph
fetched_at: 2026-10-15T19:15:54.358166+00:00
---

# Gemini Credentials API  |  Gemini API  |  Google AI for Developers

> Source: https://ai.google.dev/api/credentials/

Gemini 4 Argon is now available. [Try it out](https://aistudio.google.com/prompts/new_chat?model=gemini-4-argon). 

  * [ Home ](https://ai.google.dev/)
  * [ Gemini API ](https://ai.google.dev/gemini-api)
  * [ API reference ](https://ai.google.dev/api)



Send feedback 

#  Gemini Credentials API

The Credentials API allows you to create, retrieve, update, list, and delete server-managed credentials (such as API keys, OAuth2 tokens, HTTP Bearer tokens, and environment variables) to authenticate tool calls and MCP servers.

[View as markdown](https://ai.google.dev/static/api/credentials.md.txt) [View the OpenAPI Spec](https://ai.google.dev/static/api/interactions.openapi.json)

This API is in Beta. Endpoints are under `/v1beta/`.

## CreateCredential

post  https://generativelanguage.googleapis.com/v1beta/credentials 

Creates a new credential.

  * Request body
  * Response



### Request body

The request body structure depends on the interaction mode you choose:

EnvironmentVariableConfig 

Configuration for environment variable credentials.

id string (required)

No description provided.

injection_location InjectionLocation or array (InjectionLocation) (required)

Required. Locations where the environment variable can be injected in outgoing HTTP requests. Must contain at least one location. Accepts either a single location (e.g. "header") or an array of locations.

#### Possible values

  * `header`

Injected into HTTP request headers.

  * `query`

Injected into HTTP URL query parameters.

  * `body`

Injected into HTTP request body.




trusted_domains array (string) (optional)

Optional. List of domains allowed to receive this environment variable value in HTTP requests.

type object (required)

No description provided.

value string (required)

Required. Input only. Secret value of the environment variable. Write-only; never returned in responses.

HttpBearerConfig 

Configuration for HTTP Bearer token credentials.

header_name string (optional)

Optional. Header name to inject the token into. Defaults to 'Authorization'.

id string (required)

No description provided.

prefix string (optional)

Optional. Prefix to prepend to the token. Defaults to 'Bearer'. Set to '' for no prefix.

token string (required)

Required. Input only. The static bearer token. Write-only; never returned in responses.

type object (required)

No description provided.

OAuth2Config 

Configuration for OAuth2 credentials with automatic token refresh.

client_id string (required)

Required. OAuth2 client ID.

client_secret string (required)

Required. Input only. OAuth2 client secret. Write-only; never returned in responses.

id string (required)

No description provided.

refresh_token string (required)

Required. Input only. OAuth2 refresh token. Write-only; never returned in responses.

scopes array (string) (optional)

Optional. List of OAuth2 scopes.

token_url string (required)

Required. OAuth2 token endpoint URL for refreshing access tokens.

type object (required)

No description provided.

### Response

If successful, the response body contains data with the following structure:

create_time string (optional)

Output only. The timestamp when the credential was created.

id string (optional)

Required. Output only. Identifier. Unique identifier for the credential.

status enum (string) (optional)

Output only. Current status of the credential.

Possible values:

  * `active`

The credential is active and valid for use.

  * `revoked`

The credential has been revoked and is no longer valid.




type enum (string) (optional)

Required. Output only. The type of credential.

Possible values:

  * `bearer_token`

Static token injected as header. No refresh logic.

  * `oauth2`

Auto-refresh expired access tokens using stored refresh token.

  * `environment_variable`

Environment variable injected into sandbox container.




update_time string (optional)

Output only. The timestamp when the credential was last updated.

### Example

####  Example Response
    
    
    {
      "create_time": "string",
      "id": "string",
      "status": "active",
      "type": "bearer_token",
      "update_time": "string"
    }

## ListCredentials

get  https://generativelanguage.googleapis.com/v1beta/credentials 

Lists credentials.

  * Path / Query parameters
  * Response



### Path / Query Parameters

page_size integer (optional)

Optional. Maximum number of credentials to return.

page_token string (optional)

Optional. Pagination token.

### Response

If successful, the response body contains data with the following structure:

credentials array (Credential) (optional)

No description provided.

next_page_token string (optional)

No description provided.

### Example

####  Example Response
    
    
    {
      "credentials": [
        {
          "create_time": "string",
          "id": "string",
          "status": "active",
          "type": "bearer_token",
          "update_time": "string"
        }
      ],
      "next_page_token": "string"
    }

## GetCredential

get  https://generativelanguage.googleapis.com/v1beta/credentials/{id} 

Gets a credential by ID.

  * Path / Query parameters
  * Response



### Path / Query Parameters

id string (required)

Required. Resource ID segment making up resource `name`. It identifies the resource within its parent collection as described in https://google.aip.dev/122.

### Response

If successful, the response body contains data with the following structure:

create_time string (optional)

Output only. The timestamp when the credential was created.

id string (optional)

Required. Output only. Identifier. Unique identifier for the credential.

status enum (string) (optional)

Output only. Current status of the credential.

Possible values:

  * `active`

The credential is active and valid for use.

  * `revoked`

The credential has been revoked and is no longer valid.




type enum (string) (optional)

Required. Output only. The type of credential.

Possible values:

  * `bearer_token`

Static token injected as header. No refresh logic.

  * `oauth2`

Auto-refresh expired access tokens using stored refresh token.

  * `environment_variable`

Environment variable injected into sandbox container.




update_time string (optional)

Output only. The timestamp when the credential was last updated.

### Example

####  Example Response
    
    
    {
      "create_time": "string",
      "id": "string",
      "status": "active",
      "type": "bearer_token",
      "update_time": "string"
    }

## UpdateCredential

patch  https://generativelanguage.googleapis.com/v1beta/credentials/{id} 

Updates a credential.

  * Path / Query parameters
  * Request body
  * Response



### Path / Query Parameters

id string (required)

Required. Resource ID segment making up resource `name`. It identifies the resource within its parent collection as described in https://google.aip.dev/122.

update_mask string (optional)

Optional. The list of fields to update.

### Request body

The request body structure depends on the interaction mode you choose:

EnvironmentVariableUpdateConfig 

Configuration for updating environment variable credentials.

injection_location InjectionLocation or array (InjectionLocation) (optional)

Optional. Locations where the environment variable can be injected in outgoing HTTP requests. Accepts either a single location (e.g. "header") or an array of locations.

#### Possible values

  * `header`

Injected into HTTP request headers.

  * `query`

Injected into HTTP URL query parameters.

  * `body`

Injected into HTTP request body.




trusted_domains array (string) (optional)

Optional. List of domains allowed to receive this environment variable value in HTTP requests.

type object (required)

No description provided.

value string (optional)

Optional. Input only. Secret value of the environment variable. Write-only; never returned in responses.

HttpBearerUpdateConfig 

Configuration for updating HTTP Bearer token credentials.

header_name string (optional)

Optional. Header name to inject the token into. Defaults to 'Authorization'.

prefix string (optional)

Optional. Prefix to prepend to the token. Defaults to 'Bearer'. Set to '' for no prefix.

token string (optional)

Optional. Input only. The static bearer token. Write-only; never returned in responses.

type object (required)

No description provided.

OAuth2UpdateConfig 

Configuration for updating OAuth2 credentials.

client_id string (optional)

Optional. OAuth2 client ID.

client_secret string (optional)

Optional. Input only. OAuth2 client secret. Write-only; never returned in responses.

refresh_token string (optional)

Optional. Input only. OAuth2 refresh token. Write-only; never returned in responses.

scopes array (string) (optional)

Optional. List of OAuth2 scopes.

token_url string (optional)

Optional. OAuth2 token endpoint URL for refreshing access tokens.

type object (required)

No description provided.

### Response

If successful, the response body contains data with the following structure:

create_time string (optional)

Output only. The timestamp when the credential was created.

id string (optional)

Required. Output only. Identifier. Unique identifier for the credential.

status enum (string) (optional)

Output only. Current status of the credential.

Possible values:

  * `active`

The credential is active and valid for use.

  * `revoked`

The credential has been revoked and is no longer valid.




type enum (string) (optional)

Required. Output only. The type of credential.

Possible values:

  * `bearer_token`

Static token injected as header. No refresh logic.

  * `oauth2`

Auto-refresh expired access tokens using stored refresh token.

  * `environment_variable`

Environment variable injected into sandbox container.




update_time string (optional)

Output only. The timestamp when the credential was last updated.

### Example

####  Example Response
    
    
    {
      "create_time": "string",
      "id": "string",
      "status": "active",
      "type": "bearer_token",
      "update_time": "string"
    }

## DeleteCredential

delete  https://generativelanguage.googleapis.com/v1beta/credentials/{id} 

Deletes a credential.

  * Path / Query parameters
  * Response



### Path / Query Parameters

id string (required)

Required. Resource ID segment making up resource `name`. It identifies the resource within its parent collection as described in https://google.aip.dev/122.

### Response

If successful, the response is empty.

### Example

## Resources

### Credential

Server-managed credential resource stored in Secret Manager.

#### Fields

create_time string (optional)

Output only. The timestamp when the credential was created.

id string (optional)

Required. Output only. Identifier. Unique identifier for the credential.

status enum (string) (optional)

Output only. Current status of the credential.

Possible values:

  * `active`

The credential is active and valid for use.

  * `revoked`

The credential has been revoked and is no longer valid.




type enum (string) (optional)

Required. Output only. The type of credential.

Possible values:

  * `bearer_token`

Static token injected as header. No refresh logic.

  * `oauth2`

Auto-refresh expired access tokens using stored refresh token.

  * `environment_variable`

Environment variable injected into sandbox container.




update_time string (optional)

Output only. The timestamp when the credential was last updated.

Send feedback 

Except as otherwise noted, the content of this page is licensed under the [Creative Commons Attribution 4.0 License](https://creativecommons.org/licenses/by/4.0/), and code samples are licensed under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0). For details, see the [Google Developers Site Policies](https://developers.google.com/site-policies). Java is a registered trademark of Oracle and/or its affiliates.

Last updated 2026-09-28 UTC.

Need to tell us more?  [[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Missing the information I need","missingTheInformationINeed","thumb-down"],["Too complicated / too many steps","tooComplicatedTooManySteps","thumb-down"],["Out of date","outOfDate","thumb-down"],["Samples / code issue","samplesCodeIssue","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-09-28 UTC."],[],[]] 
