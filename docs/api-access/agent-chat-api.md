---
layout: default
title: Agent Chat API
parent: API Access
nav_order: 3
---

# API Documentation: Agent Chat API

## Endpoint

**URL:** `https://sense.lucidstack.xyz/client/api/v1/agents/{agent_id}/execute`

**Method:** `POST`

## Authentication

This API requires authentication using an API key. Include the `Authorization` header with the following format:

```
Authorization: ApiKey <your_api_key>
```

## Headers

| Header Name     | Description                    | Required |
|----------------|--------------------------------|----------|
| Authorization  | API Key for authentication     | Yes      |
| Content-Type   | Must be `application/json`     | Yes      |

## Request Body

The request body must be in JSON format with the following structure:

```json
{
    "chat_id": "<chat_id>",
    "message": "<message_text>",
    "context": {
        "user_id": "<user_id>",
        "<key_1>": "<val_1>"
    }
}
```

### Parameters

| Parameter  | Type   | Description                        | Required |
|------------|--------|------------------------------------|----------|
| chat_id    | string | Chat ID, not required for first message in the chat    | No      |
| message    | string | User's message to the agent       | Yes      |
| context    | object | Additional contextual information | No       |

## Example Request

```bash
curl --location 'https://sense.lucidstack.xyz/client/api/v1/agents/<agent_id>/execute' \
--header 'Authorization: ApiKey <your_api_key>' \
--header 'Content-Type: application/json' \
--data '{
    "chat_id": "67aacda236ba66b3082b1fe5",
    "message": "What is factorial of 6",
    "context": {
        "user_id": "123"
    }
}'
```

## Response

A successful request returns a JSON object with the following structure:

```json
{
    "chat_id": "67aacda236ba66b3082b1fe5",
    "reply": "The factorial of 6 is 720. Is there anything else you'd like to do or ask?"
}
```

### Response Fields

| Field   | Type   | Description                                  |
|---------|--------|----------------------------------------------|
| chat_id | string | The chat ID associated with the response    |
| reply   | string | The agent's reply message                   |

## Error Handling

If the request fails, the response will include an error message and a corresponding HTTP status code. Example:

```json
{
    "success": false,
    "message": "Invalid API Key"
}
```

### Common Error Codes

| Status Code | Description                          |
|-------------|--------------------------------------|
| 400         | Bad Request - Invalid input data    |
| 401         | Unauthorized - Invalid API Key     |
| 404         | Not Found - Agent or resource missing |
| 500         | Internal Server Error               |

## Notes
- Ensure that the API key is kept secure and not exposed.
- The API supports JSON request and response formats.
- Additional context can be sent as needed, depending on the use case.
