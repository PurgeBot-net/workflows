# workflows

Reusable GitHub Actions workflows for [PurgeBot-net](https://github.com/PurgeBot-net). All service and library repos call these via `workflow_call`.

## Workflows

### `build-service.yml`

Builds and pushes a Docker image to `ghcr.io` tagged with the commit SHA. Called on every push and pull request for service repos.

| Input          | Description                              |
| -------------- | ---------------------------------------- |
| `package_name` | Repository / image name (e.g. `gateway`) |

### `build-library.yml`

Runs vet and tests for library repos (no Docker image produced).

### `auto-label.yaml`

Labels pull requests based on the checked checkboxes in the PR body (`type:bug`, `type:feature`, etc.) and flags uncommented `replace` directives in `go.mod`.

### `validate-docker.yml`

Validates `docker-compose.yml` syntax and checks that every `${VAR}` reference in the compose file has a corresponding entry in `.env.example`.

## Usage

Reference a workflow from your repo's CI:

```yaml
jobs:
    build:
        uses: PurgeBot-net/workflows/.github/workflows/build-service.yml@main
        with:
            package_name: my-service
        secrets: inherit
```

New repos should be created from the [template](https://github.com/PurgeBot-net/template), which wires this up automatically.
