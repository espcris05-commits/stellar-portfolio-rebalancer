# Flaky Test Quarantine & Owner Re-enable Process

This document defines the process for handling flaky tests in the Stellar Portfolio Rebalancer.

## What is a Flaky Test?

A test that passes and fails without any code change — typically due to:
- Timing/race conditions
- Network dependencies
- Random data or non-deterministic ordering
- Environment-specific behavior

## Quarantine Flow

### 1. Detection

A test is considered flaky when it:
- Fails in CI but passes locally without changes
- Passes on retry without code changes
- Fails intermittently across different CI runs

### 2. Quarantine

1. Open a PR that moves the flaky test to a `__quarantine__/` directory
2. Add a comment above the test: `// QUARANTINED: <issue-link>`
3. Label the quarantine PR with `flaky-test`
4. Create a tracking issue to fix the flaky test

### 3. Owner Assignment

The person who quarantined a test is responsible for:
- Investigating the root cause
- Creating a fix within 2 weeks
- Either fixing or escalating to a maintainer

### 4. Re-enable Process

To re-enable a quarantined test:

1. **Root cause** must be identified (comment in the tracking issue)
2. **Fix** must address the root cause (not just mask it)
3. **PR** moves the test back to its original location
4. **Reviewer** must confirm the test passes consistently (3+ CI runs)

## CI Configuration

Quarantined tests should be:
- Excluded from the main CI test suite
- Run in a separate "flaky quarantine" workflow (without blocking PRs)
- Tracked with a weekly report of currently quarantined tests

## See Also

- [CONTRIBUTING.md](../CONTRIBUTING.md)
- [Maintainer Triage Guide](maintainer-triage-guide.md)
