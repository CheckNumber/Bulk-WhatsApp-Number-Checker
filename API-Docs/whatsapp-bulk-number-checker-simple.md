---
title: 'WhatsApp Bulk Number Checker API: Fast Phone Number Verification'
description: Based on the uploaded file of phone numbers, return which phone numbers have WhatsApp enabled.
---

Check the details of the WhatsApp of the input global number, whether it is whatsapp account

> Upload Detection File Code example:

```curl
curl --location 'https://api.ekycpro.com/wa/api/simple/tasks' \
--header 'X-API-Key: API-KEY' \
--form 'user_id="USER_ID"' \
--form 'file=@"input.txt"'
```

> Check Task Status Code example:

```curl
curl --location 'https://api.ekycpro.com/wa/api/simple/tasks/cs9viu7i61pkfs4oavvg?user_id=USER_ID' \
--header 'X-API-Key: API-KEY'
```

> Response for the upload detection file successful

```json
{
  "created_at": "2024-10-19T18:24:56.450567423Z",
  "updated_at": "2024-10-19T18:24:56.450567423Z",
  "task_id": "cs9viu7i61pkfs4oavvg",
  "user_id": "test",
  "status": "pending",
  "total": 0,
  "success": 0,
  "failure": 0
}
```

> Response for the processing status

```json
{
  "created_at": "2024-10-19T18:24:56.450567423Z",
  "updated_at": "2024-10-19T18:33:22.86152082Z",
  "task_id": "cs9viu7i61pkfs4oavvg",
  "user_id": "test",
  "status": "processing",
  "total": 20000,
  "success": 6724,
  "failure": 0
}
```

> Provide a response indicating the task is completed and include the download URL for the results.

```json
{
  "created_at": "2024-10-19T18:24:56.450567423Z",
  "updated_at": "2024-10-19T18:53:43.141760071Z",
  "task_id": "cs9viu7i61pkfs4oavvg",
  "user_id": "test",
  "status": "exported",
  "total": 20000,
  "success": 20000,
  "failure": 0,
  "result_url": "https://example-link-to-results.xlsx"
}
```

### Upload file request url

`POST https://api.ekycpro.com/wa/api/simple/tasks`

### Upload file request parameters

| Parameter | Description                                                                    |
| --------- | ------------------------------------------------------------------------------ |
| `user_id` | `string`, User ID                                                              |
| `file`    | `file`, Upload file, each line should contain one phone number in E.164 format |

### Check task status request url

`GET https://api.ekycpro.com/wa/api/simple/tasks/{TASK_ID}`

### Check task status request parameters

| Parameter | Description       |
| --------- | ----------------- |
| `user_id` | `string`, User ID |

### Result Fields

| Field      | Description                                | Example      |
| ---------- | ------------------------------------------ | ------------ |
| `Number`   | Phone number in E.164 format               | +41798284651 |
| `whatsapp` | Whether number has active WhatsApp account | yes, no      |

### Response Format

| Field        | Description                                                                                                                                                                   |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `created_at` | Timestamp when task was created                                                                                                                                               |
| `updated_at` | Timestamp of last task status update                                                                                                                                          |
| `task_id`    | Unique task identifier                                                                                                                                                        |
| `user_id`    | ID of user                                                                                                                                                                    |
| `status`     | Task status: <br> `pending`: Queued and waiting <br> `processing`: Currently processing <br> `completed`: Processing finished <br> `exported`: Results available for download |
| `total`      | Total phone numbers processed                                                                                                                                                 |
| `success`    | Numbers successfully identified                                                                                                                                               |
| `failure`    | Numbers that failed processing                                                                                                                                                |
| `result_url` | (Optional) Download URL for results when status is `exported`                                                                                                                 |

### Status Codes

| Status | Description                                                    |
| ------ | -------------------------------------------------------------- |
| `200`  | `charge`, Request successful, task created or status retrieved |
| `400`  | `free`, Bad request, invalid parameters or file format         |
| `500`  | `free`, Internal server error, retry later                     |
