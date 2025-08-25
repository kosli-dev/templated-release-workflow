# Kosli Policies Action

This custom GitHub Action creates Kosli policies from YAML files in the action directory.

## Usage

```yaml
- name: Create Kosli Policies
  uses: ./kosli-policies-action
  with:
    policy_files: "artifact-provenance,trail-compliance,all-test-cases-present"
```

## Inputs

- `policy_files` (required): Comma-separated list of policy file names without extension. The action will automatically append `.yaml` and look for these files in the action directory.
- `build_id` (optional): The ID of the build to check (retained for compatibility).

## Available Policy Files

The action includes the following policy files:

- `artifact-provenance.yaml` - Requires artifacts to have provenance information (use: `artifact-provenance`)
- `trail-compliance.yaml` - Requires trail compliance (use: `trail-compliance`)
- `all-test-cases-present.yaml` - Requires specific test attestations (use: `all-test-cases-present`)

## How it works

1. The action takes a comma-separated list of policy names (without .yaml extension)
2. For each name, it appends `.yaml` to create the filename
3. Creates the policy using `kosli create policy <policy-name> <policy-file>`
4. If any policy file is not found, the action fails with an error

## Example

```yaml
- name: Create multiple policies
  uses: ./kosli-policies-action
  with:
    policy_files: "artifact-provenance,trail-compliance"
```

This will create two policies:

- `artifact-provenance` from `artifact-provenance.yaml`
- `trail-compliance` from `trail-compliance.yaml`
