---
url: https://ai.google.dev/api/webhooks/
title: Gemini Webhooks API \u00a0|\u00a0 Gemini API \u00a0|\u00a0 Google AI for Developers
method: scrapling+scrapegraph
fetched_at: 2026-10-15T19:16:04.201224+00:00
---

# Gemini Webhooks API  |  Gemini API  |  Google AI for Developers

> Source: https://ai.google.dev/api/webhooks/

Gemini 4 Argon is now available. [Try it out](https://aistudio.google.com/prompts/new_chat?model=gemini-4-argon). 

  * [ Home ](https://ai.google.dev/)
  * [ Gemini API ](https://ai.google.dev/gemini-api)
  * [ API reference ](https://ai.google.dev/api)



Send feedback 

#  Gemini Webhooks API

Webhooks allow the Gemini API to push real-time notifications to your server when asynchronous or Long-Running Operations (LROs) complete. This replaces the need to poll the API for status updates, reducing latency and overhead.

[View as markdown](https://ai.google.dev/static/api/webhooks.md.txt) [View the OpenAPI Spec](https://ai.google.dev/static/api/interactions.openapi.json)

This API is in Beta. Endpoints are under `/v1beta/`.

## CreateWebhook

post  https://generativelanguage.googleapis.com/v1beta/webhooks 

Creates a new Webhook.

  * Request body
  * Response



### Request body

The request body contains data with the following structure:

name string (optional)

Optional. The user-provided name of the webhook.

subscribed_events array (enum (string)) (required)

Required. The events that the webhook is subscribed to. Available events: \- batch.succeeded \- batch.expired \- batch.failed \- interaction.requires_action \- interaction.completed \- interaction.failed \- video.generated

Possible values:

  * `batch.succeeded`

Batch processing finished successfully.

  * `batch.expired`

Batch has not been processed within the 48h timeframe.

  * `batch.failed`

Batch job failed.

  * `interaction.requires_action`

Interaction requires action (e.g., function calling).

  * `interaction.completed`

Interaction completed successfully.

  * `interaction.failed`

Interaction failed.

  * `video.generated`

Video generation completed.




uri string (required)

Required. The URI to which webhook events will be sent.

### Response

If successful, the response body contains data with the following structure:

create_time string (optional)

Output only. The timestamp when the webhook was created.

id string (optional)

Output only. The ID of the webhook.

name string (optional)

Optional. The user-provided name of the webhook.

new_signing_secret string (optional)

Output only. The new signing secret for the webhook. Only populated on create.

signing_secrets array (SigningSecret) (optional)

Output only. The signing secrets associated with this webhook.

Represents a signing secret used to verify webhook payloads.

#### Fields

expire_time string (optional)

Output only. The expiration date of the signing secret.

truncated_secret string (optional)

Output only. The truncated version of the signing secret.

state enum (string) (optional)

Output only. The state of the webhook.

Possible values:

  * `enabled`

The webhook is enabled.

  * `disabled`

The webhook is disabled by the user.

  * `disabled_due_to_failed_deliveries`

The webhook is disabled due to failed deliveries.




subscribed_events array (enum (string)) (optional)

Required. The events that the webhook is subscribed to. Available events: \- batch.succeeded \- batch.expired \- batch.failed \- interaction.requires_action \- interaction.completed \- interaction.failed \- video.generated

Possible values:

  * `batch.succeeded`

Batch processing finished successfully.

  * `batch.expired`

Batch has not been processed within the 48h timeframe.

  * `batch.failed`

Batch job failed.

  * `interaction.requires_action`

Interaction requires action (e.g., function calling).

  * `interaction.completed`

Interaction completed successfully.

  * `interaction.failed`

Interaction failed.

  * `video.generated`

Video generation completed.




update_time string (optional)

Output only. The timestamp when the webhook was last updated.

uri string (optional)

Required. The URI to which webhook events will be sent.

### Example

####  Example Response
    
    
    {
      "create_time": "string",
      "id": "string",
      "name": "string",
      "new_signing_secret": "string",
      "signing_secrets": [
        {
          "expire_time": "string",
          "truncated_secret": "string"
        }
      ],
      "state": "enabled",
      "subscribed_events": [
        "batch.succeeded"
      ],
      "update_time": "string",
      "uri": "string"
    }

## PingWebhook

post  https://generativelanguage.googleapis.com/v1beta/webhooks/{id}:ping 

Sends a ping event to a Webhook.

  * Path / Query parameters
  * Request body
  * Response



### Path / Query Parameters

id string (required)

Required. The ID of the webhook to ping.

### Request body

The request body contains data with the following structure:

### Response

If successful, the response is empty.

### Example

## RotateSigningSecret

post  https://generativelanguage.googleapis.com/v1beta/webhooks/{id}:rotateSigningSecret 

Generates a new signing secret for a Webhook.

  * Path / Query parameters
  * Request body
  * Response



### Path / Query Parameters

id string (required)

Required. The ID of the webhook for which to generate a signing secret.

### Request body

The request body contains data with the following structure:

revocation_behavior enum (string) (optional)

Optional. The revocation behavior for previous signing secrets.

Possible values:

  * `revoke_previous_secrets_after_h24`

Generate a new signing secret and revoke all previous secrets after 24 hours. Default and safest option for migrations.

  * `revoke_previous_secrets_immediately`

Revoke all previous secrets immediately. Use with caution as this can interrupt ongoing notifications.




### Response

If successful, the response body contains data with the following structure:

secret string (optional)

Output only. The newly generated signing secret.

### Example

####  Example Response
    
    
    {
      "secret": "string"
    }

## ListWebhooks

get  https://generativelanguage.googleapis.com/v1beta/webhooks 

Lists all Webhooks.

  * Path / Query parameters
  * Response



### Path / Query Parameters

page_size integer (optional)

Optional. The maximum number of webhooks to return. The service may return fewer than this value. If unspecified, at most 50 webhooks will be returned. The maximum value is 1000.

page_token string (optional)

Optional. A page token, received from a previous `ListWebhooks` call. Provide this to retrieve the subsequent page.

### Response

If successful, the response body contains data with the following structure:

next_page_token string (optional)

A token, which can be sent as `page_token` to retrieve the next page. If this field is omitted, there are no subsequent pages.

webhooks array (Webhook) (optional)

The webhooks.

### Example

####  Example Response
    
    
    {
      "next_page_token": "string",
      "webhooks": [
        {
          "create_time": "string",
          "id": "string",
          "name": "string",
          "new_signing_secret": "string",
          "signing_secrets": [
            {
              "expire_time": "string",
              "truncated_secret": "string"
            }
          ],
          "state": "enabled",
          "subscribed_events": [
            "batch.succeeded"
          ],
          "update_time": "string",
          "uri": "string"
        }
      ]
    }

## GetWebhook

get  https://generativelanguage.googleapis.com/v1beta/webhooks/{id} 

Gets a specific Webhook.

  * Path / Query parameters
  * Response



### Path / Query Parameters

id string (required)

Required. The ID of the webhook to retrieve.

### Response

If successful, the response body contains data with the following structure:

create_time string (optional)

Output only. The timestamp when the webhook was created.

id string (optional)

Output only. The ID of the webhook.

name string (optional)

Optional. The user-provided name of the webhook.

new_signing_secret string (optional)

Output only. The new signing secret for the webhook. Only populated on create.

signing_secrets array (SigningSecret) (optional)

Output only. The signing secrets associated with this webhook.

Represents a signing secret used to verify webhook payloads.

#### Fields

expire_time string (optional)

Output only. The expiration date of the signing secret.

truncated_secret string (optional)

Output only. The truncated version of the signing secret.

state enum (string) (optional)

Output only. The state of the webhook.

Possible values:

  * `enabled`

The webhook is enabled.

  * `disabled`

The webhook is disabled by the user.

  * `disabled_due_to_failed_deliveries`

The webhook is disabled due to failed deliveries.




subscribed_events array (enum (string)) (optional)

Required. The events that the webhook is subscribed to. Available events: \- batch.succeeded \- batch.expired \- batch.failed \- interaction.requires_action \- interaction.completed \- interaction.failed \- video.generated

Possible values:

  * `batch.succeeded`

Batch processing finished successfully.

  * `batch.expired`

Batch has not been processed within the 48h timeframe.

  * `batch.failed`

Batch job failed.

  * `interaction.requires_action`

Interaction requires action (e.g., function calling).

  * `interaction.completed`

Interaction completed successfully.

  * `interaction.failed`

Interaction failed.

  * `video.generated`

Video generation completed.




update_time string (optional)

Output only. The timestamp when the webhook was last updated.

uri string (optional)

Required. The URI to which webhook events will be sent.

### Example

####  Example Response
    
    
    {
      "create_time": "string",
      "id": "string",
      "name": "string",
      "new_signing_secret": "string",
      "signing_secrets": [
        {
          "expire_time": "string",
          "truncated_secret": "string"
        }
      ],
      "state": "enabled",
      "subscribed_events": [
        "batch.succeeded"
      ],
      "update_time": "string",
      "uri": "string"
    }

## UpdateWebhook

patch  https://generativelanguage.googleapis.com/v1beta/webhooks/{id} 

Updates an existing Webhook.

  * Path / Query parameters
  * Request body
  * Response



### Path / Query Parameters

id string (required)

Required. The ID of the webhook to update.

update_mask string (optional)

Optional list of fields to update.

### Request body

The request body contains data with the following structure:

name string (optional)

Optional. The user-provided name of the webhook.

state enum (string) (optional)

Optional. The state of the webhook.

Possible values:

  * `enabled`

The webhook is enabled.

  * `disabled`

The webhook is disabled by the user.

  * `disabled_due_to_failed_deliveries`

The webhook is disabled due to failed deliveries.




subscribed_events array (enum (string)) (optional)

Optional. The events that the webhook is subscribed to. Available events: \- batch.succeeded \- batch.expired \- batch.failed \- interaction.requires_action \- interaction.completed \- interaction.failed \- video.generated

Possible values:

  * `batch.succeeded`

Batch processing finished successfully.

  * `batch.expired`

Batch has not been processed within the 48h timeframe.

  * `batch.failed`

Batch job failed.

  * `interaction.requires_action`

Interaction requires action (e.g., function calling).

  * `interaction.completed`

Interaction completed successfully.

  * `interaction.failed`

Interaction failed.

  * `video.generated`

Video generation completed.




uri string (optional)

Optional. The URI to which webhook events will be sent.

### Response

If successful, the response body contains data with the following structure:

create_time string (optional)

Output only. The timestamp when the webhook was created.

id string (optional)

Output only. The ID of the webhook.

name string (optional)

Optional. The user-provided name of the webhook.

new_signing_secret string (optional)

Output only. The new signing secret for the webhook. Only populated on create.

signing_secrets array (SigningSecret) (optional)

Output only. The signing secrets associated with this webhook.

Represents a signing secret used to verify webhook payloads.

#### Fields

expire_time string (optional)

Output only. The expiration date of the signing secret.

truncated_secret string (optional)

Output only. The truncated version of the signing secret.

state enum (string) (optional)

Output only. The state of the webhook.

Possible values:

  * `enabled`

The webhook is enabled.

  * `disabled`

The webhook is disabled by the user.

  * `disabled_due_to_failed_deliveries`

The webhook is disabled due to failed deliveries.




subscribed_events array (enum (string)) (optional)

Required. The events that the webhook is subscribed to. Available events: \- batch.succeeded \- batch.expired \- batch.failed \- interaction.requires_action \- interaction.completed \- interaction.failed \- video.generated

Possible values:

  * `batch.succeeded`

Batch processing finished successfully.

  * `batch.expired`

Batch has not been processed within the 48h timeframe.

  * `batch.failed`

Batch job failed.

  * `interaction.requires_action`

Interaction requires action (e.g., function calling).

  * `interaction.completed`

Interaction completed successfully.

  * `interaction.failed`

Interaction failed.

  * `video.generated`

Video generation completed.




update_time string (optional)

Output only. The timestamp when the webhook was last updated.

uri string (optional)

Required. The URI to which webhook events will be sent.

### Example

####  Example Response
    
    
    {
      "create_time": "string",
      "id": "string",
      "name": "string",
      "new_signing_secret": "string",
      "signing_secrets": [
        {
          "expire_time": "string",
          "truncated_secret": "string"
        }
      ],
      "state": "enabled",
      "subscribed_events": [
        "batch.succeeded"
      ],
      "update_time": "string",
      "uri": "string"
    }

## DeleteWebhook

delete  https://generativelanguage.googleapis.com/v1beta/webhooks/{id} 

Deletes a Webhook.

  * Path / Query parameters
  * Response



### Path / Query Parameters

id string (required)

Required. The ID of the webhook to delete.

### Response

If successful, the response is empty.

### Example

## Resources

### Webhook

A Webhook resource.

#### Fields

create_time string (optional)

Output only. The timestamp when the webhook was created.

id string (optional)

Output only. The ID of the webhook.

name string (optional)

Optional. The user-provided name of the webhook.

new_signing_secret string (optional)

Output only. The new signing secret for the webhook. Only populated on create.

signing_secrets array (SigningSecret) (optional)

Output only. The signing secrets associated with this webhook.

Represents a signing secret used to verify webhook payloads.

#### Fields

expire_time string (optional)

Output only. The expiration date of the signing secret.

truncated_secret string (optional)

Output only. The truncated version of the signing secret.

state enum (string) (optional)

Output only. The state of the webhook.

Possible values:

  * `enabled`

The webhook is enabled.

  * `disabled`

The webhook is disabled by the user.

  * `disabled_due_to_failed_deliveries`

The webhook is disabled due to failed deliveries.




subscribed_events array (enum (string)) (optional)

Required. The events that the webhook is subscribed to. Available events: \- batch.succeeded \- batch.expired \- batch.failed \- interaction.requires_action \- interaction.completed \- interaction.failed \- video.generated

Possible values:

  * `batch.succeeded`

Batch processing finished successfully.

  * `batch.expired`

Batch has not been processed within the 48h timeframe.

  * `batch.failed`

Batch job failed.

  * `interaction.requires_action`

Interaction requires action (e.g., function calling).

  * `interaction.completed`

Interaction completed successfully.

  * `interaction.failed`

Interaction failed.

  * `video.generated`

Video generation completed.




update_time string (optional)

Output only. The timestamp when the webhook was last updated.

uri string (optional)

Required. The URI to which webhook events will be sent.

Send feedback 

Except as otherwise noted, the content of this page is licensed under the [Creative Commons Attribution 4.0 License](https://creativecommons.org/licenses/by/4.0/), and code samples are licensed under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0). For details, see the [Google Developers Site Policies](https://developers.google.com/site-policies). Java is a registered trademark of Oracle and/or its affiliates.

Last updated 2026-09-28 UTC.

Need to tell us more?  [[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Missing the information I need","missingTheInformationINeed","thumb-down"],["Too complicated / too many steps","tooComplicatedTooManySteps","thumb-down"],["Out of date","outOfDate","thumb-down"],["Samples / code issue","samplesCodeIssue","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-09-28 UTC."],[],[]] 
