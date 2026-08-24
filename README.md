# KyrboForge Actions

Small, reusable GitHub Actions maintained by KyrboForge.

## `release-token`

Creates a short-lived installation token for the KyrboForge release GitHub
App, scoped to the repository running the workflow.

### Organization setup

Configure these values under **KyrboForge → Settings → Secrets and
variables → Actions** and grant the target repositories access:

- variable `RELEASE_APP_CLIENT_ID` — the GitHub App client ID;
- secret `RELEASE_APP_PRIVATE_KEY` — the complete generated PEM private key.

Install the GitHub App on each target repository and add it to the relevant
ruleset bypass list.

### Usage

```yaml
- uses: KyrboForge/actions/release-token@<full-commit-sha>
  id: release-token
  with:
    client-id: ${{ vars.RELEASE_APP_CLIENT_ID }}
    private-key: ${{ secrets.RELEASE_APP_PRIVATE_KEY }}

- uses: actions/checkout@v7
  with:
    ref: main
    fetch-depth: 0
    token: ${{ steps.release-token.outputs.token }}
```

The token is revoked automatically when the job finishes. Keep subsequent
steps that use it in the same job.

## Versioning

Consumers should pin the action to a full commit SHA.

## License

Licensed under the [MIT License](LICENSE).
