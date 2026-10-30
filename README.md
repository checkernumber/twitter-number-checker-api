# X (Twitter) Number Checker API — official examples | CheckNumber

This repository documents the CheckNumber X (Twitter) Number Checker API integration contract.

- Product page: https://checknumber.ai/products/x-twitter
- API base URL: `https://api.checknumber.ai`
- Authentication: `X-API-Key`
- API key environment variable: `CHECKNUMBER_API_KEY`
- License: MIT

## Processing model

This is a file-based asynchronous API. Submit an authorized text file, poll the task until `exported`, then download the result URL. It is not a realtime single-identifier endpoint.

```bash
curl -X POST "https://api.checknumber.ai/v1/tasks" -H "X-API-Key: ${CHECKNUMBER_API_KEY}" -F "file=@examples/numbers.txt" -F "task_type=twitter"
curl -X POST "https://api.checknumber.ai/v1/gettasks" -H "X-API-Key: ${CHECKNUMBER_API_KEY}" -F "task_id=YOUR_TASK_ID"
```

## Products and limits

| Code | Name | Input | Limits | Result fields | Documentation |
| --- | --- | --- | --- | --- | --- |
| `twitter` | Number Checker | phone | 1–10,000,000 upload rows; billing floor 500 | `number, activated` | [local OpenAPI](openapi.yaml) |
| `twitter_email` | Email Checker | email | 1–10,000,000 upload rows; billing floor 500 | `email, activated` | [docs](https://docs.checknumber.ai/twitter-email-checker) |

## Response and boundaries

- Interpret exported CSV rows only after the task is exported. A failed request, missing field or unavailable result is not a confirmed negative; preserve the exported values rather than applying a synchronous-batch `exists` rule.
- Authentication keys must come from environment variables or a secret manager; never commit keys or call private/internal endpoints.
- Product prices can change. Check the official pricing page at runtime; this repository intentionally does not hard-code a price.
- Use only identifiers you are authorized to process and follow applicable privacy, platform, and data-protection requirements.

## Runnable examples

Seven self-contained examples are provided under `examples/`: Python, Node.js, Go, Java, C#, PHP, and Shell each implement the full submit → poll → download workflow with HTTP error handling. Set the server-side API-key environment variable before running them.

## Official resources

- `twitter`: openapi.yaml
- `twitter_email`: https://docs.checknumber.ai/twitter-email-checker
- Pricing: https://checknumber.ai/pricing
- OpenAPI contract: [openapi.yaml](openapi.yaml)

Last reviewed: 2026-10-30.

## Upload and billing limits verified 2026-10-30

- `twitter`: upload 1–10,000,000 entries; minimum billable quantity 500.
- `twitter_email`: upload 1–10,000,000 entries; minimum billable quantity 500.

Upload minimum and minimum billable quantity are different. A smaller accepted upload can still be billed at the stated minimum; a wholly failed task with zero processed entries is not charged a minimum. A billable quantity of 0 means no billing floor. Check current pricing before submitting.

## Hosted product guide

The previous product-specific hosted guide is unavailable. The local [OpenAPI contract](openapi.yaml) and this repository’s request/response facts are the integration reference for this product. An unrelated product page is not a substitute.

Get an API key: https://platform.checknumber.ai?utm_source=github&utm_medium=referral&utm_campaign=checkernumber_twitter-number-checker-api
