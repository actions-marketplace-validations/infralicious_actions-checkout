# 0005: Human review stays, no full automation

- Status: Accepted
- Date: 2026-10-26

## Context

Test, Upstream-check, Scorecard, and Renovate run automatically.
Safe-settings sync runs from the admin repo.
A human still reviews Renovate PRs.
A human still creates signed tags.
A human still creates releases.
A human still pushes after approval.

## Decision

Keep human review for this security action.
Automation never changes an input default by itself.
Automation never creates a tag.
Automation never creates a release.
Automation never merges without human review.

## Consequences

Upstream changes ship only after human review.
Tags stay SSH signed by the user.
Releases stay immutable and verified.
A bad upstream change cannot auto-ship to users.
Work stays slower than full automation, by design.

## Rejected alternatives

Auto merge: ships upstream changes without review.
Auto tag: tag would not be SSH signed by the user.
Auto release: release could ship a wrong SHA or wrong default.
