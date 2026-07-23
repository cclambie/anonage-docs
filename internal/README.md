# Internal API surface — not published

`openapi-internal.json` holds the endpoints that are **deliberately excluded** from
docs.anonage.io: the ones the AnonAge web app, mobile wallet and identity provider use, which no
merchant ever calls.

| Group | Endpoints | Why it is internal |
|---|---|---|
| Users | profile, change password, change email, delete account | Account management inside our own apps. |
| KYC | applicant, check, status, SDK token, hosted link | Identity-provider plumbing. Names our provider and its flow. |
| API keys | create, list, revoke | Merchants create keys in the Dashboard UI, not over the API. |
| Webhooks | inbound provider webhook | Our own callback receiver, not a merchant integration point. |

The **public** spec (`../api-reference/openapi.json`) is what `docs.json` renders, and covers only
Health, Auth, Verification and Usage.

## Keeping the two in sync

Both are generated from the same source by tagging: an operation tagged `Health`, `Auth`,
`Verification` or `Usage` is public, anything else is internal. When you add an endpoint, tag it and
put it in the matching file.

## Publishing these internally (later)

The plan is a second, access-controlled Mintlify project pointed at this directory. Nothing here is
wired into `docs.json`, so files in `internal/` are never built or served today.
