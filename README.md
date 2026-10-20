# Detection negative fixture: weak YAML matches

This branch deliberately contains text that matches the content-search marker
for Compose but is not a Compose file.

- `README.md` has an incomplete example inside a Markdown fence.
- `banana` has the same incomplete YAML without a recognised Compose name.

Expected result from `POST /api/v3/app/detections` after polling:

```text
status: failed
result: null
error.code: NO_SUPPORTED_APPLICATIONS
```

Neither file may be offered as a Dockerfile or Docker Compose entrypoint.

```yaml
services: [
```
