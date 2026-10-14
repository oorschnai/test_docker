# Custom Dockerfile and Compose path smoke tests

This branch contains small fixtures for testing all three `build_entry_path`
forms in Apps: omitted/null, a directory, and an exact file. Every fixture has
a different marker, so an unexpected fallback to the root entrypoint is visible.

Run one backend application at a time on the test VDS.

## Docker

Legacy/default form:

```text
build_entry_path = null
```

Apps must use the root `Dockerfile`. Its page contains
`docker-default-path-ok`.

Directory form:

```text
build_entry_path = docker/directory
```

Expected entrypoint and build context:

```text
Dockerfile: docker/directory/Dockerfile
context:    docker/directory
```

Exact-file form:

```text
build_entry_path = docker/приложение/мой файл
```

Expected entrypoint and build context:

```text
Dockerfile: docker/приложение/мой файл
context:    docker/приложение
```

Both images expose port `8080`. Their root pages contain different markers:

- `docker-directory-path-ok`
- `docker-exact-path-ok`

## Docker Compose

Legacy/default form:

```text
build_entry_path = null
```

Apps must use the root `compose.yaml`. The service publishes host port `18082`
and has `PATH_TEST_MARKER=compose-default-path-ok`.

Directory form:

```text
build_entry_path = compose/directory
```

Apps must select `compose/directory/compose.yaml`. The service publishes host
port `18080` and has `PATH_TEST_MARKER=compose-directory-path-ok`.

Exact-file form:

```text
build_entry_path = compose/producción/mi archivo
```

Apps must use that exact extensionless file. The service publishes host port
`18081` and has `PATH_TEST_MARKER=compose-exact-path-ok`.

The exact Compose path should also be used by pause, resume, reboot, rollback,
and cleanup operations. If an explicit-path deployment exposes a default
marker instead, Apps incorrectly fell back to the root entrypoint.
