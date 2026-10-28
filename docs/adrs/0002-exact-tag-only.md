# 0002: Exact tag only, no floating major tag

- Status: Accepted
- Date: 2026-10-26

## Context

Repo tag matches upstream tag exactly.
A floating major tag must move on each release.
An immutable release locks its tag to one commit.
These two rules cannot both hold.
Tag protection blocks tag deletion, update, and non fast forward.
Safe-settings manages Tag protection now.

## Decision

This repo uses exact tags only.
No floating major tag exists in this repo.
A new tag ships only with a new upstream tag.
A shipped tag stays at its commit forever.

## Consequences

Users pin a known version, not a moving tag.
Marketplace listing shows the tag README, not main README.
README changes reach Marketplace only on a new release.
Deleting an immutable release burns its tag name forever.
The same tag name can never be reused, even after repo deletion.

## Rejected alternatives

Floating v7 tag: moves on each release, breaks immutable releases.
Moving a tag by hand: needs ruleset disable first, then restore.
