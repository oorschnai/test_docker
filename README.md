# Detection negative fixture: unsupported Compose tag

`custom-compose` is intentionally extensionless and has a valid Compose-like
structure, so it must be found by content search. Its `!reset` tag is not
supported by the current Agent and must be rejected locally before the model
can offer it as an entrypoint.

Expected result from `POST /api/v3/app/detections` after polling:

```text
status: failed
result: null
error.code: APPLICATION_CONFIGURATION_UNRESOLVED
```

There must be no ready Dockerfile or Docker Compose candidate.
