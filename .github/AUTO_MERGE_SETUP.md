# Dependabot Auto-Merge Setup

This repository is configured with automatic merging of Dependabot pull requests when tests pass.

## How it works

1. **Dependabot Configuration** (`.github/dependabot.yml`):
   - Checks for Maven dependency updates weekly on Mondays
   - Groups related dependencies together to reduce PR noise
   - Limits to 10 open PRs at a time
   - Ignores major version updates for critical dependencies

2. **Auto-Merge Workflow** (`.github/workflows/dependabot-auto-merge.yml`):
   - Triggers only on PRs created by `dependabot[bot]`
   - Runs the full test suite using Maven (`./mvnw clean test`)
   - Builds the project to ensure compilation succeeds
   - Checks if the PR is in a mergeable state
   - Auto-approves the PR if tests pass
   - Enables auto-merge with merge commit strategy

3. **CI Workflow** (`.github/workflows/ci.yml`):
   - Runs on all PRs and pushes to main/master
   - Provides comprehensive testing for all changes
   - Includes build, test, and package steps

## Safety Features

- **Test Requirement**: PRs are only merged if all tests pass
- **Build Verification**: Ensures the project compiles successfully
- **Mergeable Check**: Verifies the PR can be safely merged
- **Dependency Grouping**: Related dependencies are updated together
- **Major Version Protection**: Major updates for critical dependencies require manual review

## Manual Override

If you need to prevent auto-merge for a specific Dependabot PR:
1. Add a `do-not-merge` label to the PR
2. Close and reopen the PR (this will require manual review)
3. Convert the PR to draft status

## Monitoring

- Check the Actions tab for workflow execution status
- Review the Dependabot security tab for vulnerability updates
- Monitor the dependency graph for outdated packages

## Configuration

To modify the auto-merge behavior:
- Edit `.github/dependabot.yml` for dependency update settings
- Edit `.github/workflows/dependabot-auto-merge.yml` for merge logic
- Edit `.github/workflows/ci.yml` for general CI behavior