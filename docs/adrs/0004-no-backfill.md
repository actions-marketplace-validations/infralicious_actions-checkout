# 0004: No backfill, fill only newer releases

- Status: Accepted
- Date: 2026-10-27

## Context

Upstream v7.0.0 exists, but this repo has no v7.0.0 release.
This repo has only v7.0.1, as an immutable release.
A backfill test would create a v7.0.0 tag and release.
That test would not prove the real upgrade flow.
The real upgrade flow happens on a newer upstream release.

## Decision

Do not backfill older upstream tags.
Fill only newer upstream releases.
When upstream releases a newer tag, create a matching signed tag.
Create an immutable release for that tag.
Release notes must link to the upstream release.
Publish that release on Marketplace through the UI.

## Consequences

Older upstream versions stay unfilled in this repo.
v7.0.1 stays latest until a newer upstream release ships.
Marketplace README stays old until a newer publish ships.
No tag name is burned for a test release.
The first real upgrade tests Renovate, tag, release, and Marketplace together.

## Rejected alternatives

Backfill v7.0.0: proves tag and release, but adds an old version.
Delete v7.0.1 to test v7.0.0: burns v7.0.1 tag name forever.
