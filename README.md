# API Breaking Change Detector

CI-native OpenAPI compatibility checking: diff two spec versions and flag breaking
changes - removed endpoints, removed response fields, new required request fields,
type changes, enum shrinkage - with severity-tagged reports posted to the PR.

## How it works

    openapi-diff old.yaml new.yaml --format markdown
    -> exits 1 if any ERROR-severity breaking change exists

## Severity rules

| Severity | Example |
|---|---|
| ERROR (breaking) | endpoint removed, response field removed, new required request field, type changed, enum value removed |
| WARNING | field deprecated, optional field added to response |
| INFO | new optional request field |

## GitHub Actions usage

    - uses: ./            # or your published action
      with:
        base: openapi.v1.yaml
        head: openapi.yaml

Posts the report as a PR comment and fails the check on ERRORs.
