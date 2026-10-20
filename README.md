# Detection fixture: source-path policy

This branch contains four Dockerfile-shaped files whose names exercise the
publishable-path rules.

Expected ready candidates from `POST /api/v3/app/detections` after polling:

```text
/dir/.dockerfile_path
/dir/ Dockerfile
```

The root `.dockerfile_path` is a Builder-reserved file and must never be
offered as a Dockerfile. The root file whose name starts with a space must
also be filtered instead of being normalised into another path.

The two accepted files prove that a reserved basename is allowed below the
root and that an internal space is preserved literally.
