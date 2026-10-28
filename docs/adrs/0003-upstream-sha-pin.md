# 0003: Upstream pin uses full SHA with version comment

- Status: Accepted
- Date: 2026-10-26

## Context

Upstream checkout is a third party action.
A tag pin can move without a code change.
A full SHA pin cannot move silently.
Renovate updates SHA pins, but it needs a version comment.
A bare SHA pin without a version comment is disabled by Renovate.
SHA pinning is enforced at repo level via Actions permissions.

## Decision

Action pins upstream by full SHA, not a tag.
Code SHA lines carry a version comment, for example `# v7.0.1`.
Renovate updates code SHA lines automatically.
README uses placeholders, not hardcoded versions or SHAs.
Prose, descriptions, and non-essential comments use no version or SHA.

## Consequences

Users get a known upstream commit, not a moving tag.
Renovate can propose SHA updates in a grouped PR.
README needs no update on a SHA change.
Local `./` actions are not third party actions.
SHA pinning enforcement does not block local `./` use.
All external uses in workflows use full SHA with version comment.

## Rejected alternatives

Tag pin only: simpler to read, but the tag can move.
Bare SHA pin: secure, but Renovate cannot update it.
Hardcoded versions in prose: drift on each release, now banned by rule.
