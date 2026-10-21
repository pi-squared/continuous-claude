# Local Validation Workflow

This document describes how to validate the repository locally without calling Claude Code, modifying GitHub, or requiring credentials or API keys.

## 1. Bash Syntax Check

Run these commands from the repository root. Each `bash -n` invocation checks one tracked Bash script without executing it:

```bash
bash -n continuous_claude.sh
bash -n install.sh
bash -n tests/setup.sh
```

## 2. Test Suite Execution

The existing CI workflow runs the [bats-core](https://github.com/bats-core/bats-core) unit tests. These tests use mocks for Claude and GitHub operations and require `jq` for JSON checks.

1. Download the test dependencies into `tests/libs`. This setup step requires Git and network access to public GitHub repositories; it is not an offline step:

```bash
./tests/setup.sh
```

2. Once the dependencies are present, run the unit tests:

```bash
./tests/libs/bats/bin/bats tests/test_continuous_claude.bats
```
