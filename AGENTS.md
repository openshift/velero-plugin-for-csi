# AGENTS.md — AI Agent Instructions for openshift/velero-plugin-for-csi

## Project Overview
This is the OpenShift fork of the Velero Plugin for CSI (Container Storage Interface). It enables Velero to backup and restore persistent volumes using CSI volume snapshots. The plugin leverages CSI snapshot APIs to create consistent point-in-time snapshots of volumes during backup operations. Maintained on the `oadp-dev` branch for the OADP ecosystem.

- **Primary Language**: Go
- **Module**: `github.com/vmware-tanzu/velero-plugin-for-csi`
- **Default Branch**: `oadp-dev`

## Build Instructions
```bash
# Build the plugin binary locally
make local

# Build container image
make container
```

## Test Instructions
```bash
# Run all tests
make test

# Run CI checks (modules verification + tests)
make ci

# Run specific tests
go test ./internal/... -run TestName

# Vet code
go vet ./...
```

## Module Management
```bash
# Update Go modules
make modules

# Verify modules are tidy
make verify-modules
```

## Code Conventions
- Plugin code in `internal/` directory
- Follow Velero plugin interface patterns (BackupItemAction, RestoreItemAction)
- Use CSI snapshot API types from `k8s.io/api/`
- Error handling with context wrapping
- Changelog entries in `changelogs/`
- Documentation in `doc/`

## Project Structure
```
internal/      - Plugin implementation
  backup/      - Backup item action plugins
  restore/     - Restore item action plugins
  util/        - Shared utilities
changelogs/    - Release changelog entries
doc/           - Documentation
examples/      - Example configurations
hack/          - Build and CI scripts
```

## CI/CD
- GitHub Actions workflows in `.github/workflows/`:
  - `pr.yml` — PR validation
  - `push.yml` — Push CI
  - `auto_assign_prs.yml` — Auto-assign PR reviewers
  - `auto_request_review.yml` — Auto-request reviews
- Reproduce CI locally:
  ```bash
  make ci
  ```

## Common Tasks

### Adding a new CSI backup/restore action
1. Create action in `internal/backup/` or `internal/restore/`
2. Implement the appropriate Velero plugin interface
3. Register the plugin
4. Add tests
5. Add changelog entry in `changelogs/`

### Updating OADP-specific patches
- OADP patches live on the `oadp-dev` branch
- UBI-based Dockerfile: `Dockerfile.ubi`
