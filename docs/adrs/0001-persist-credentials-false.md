# 0001: Persist-credentials defaults to false

- Status: Accepted
- Date: 2026-10-25

## Context

Upstream checkout defaults persist-credentials to true.
A persisted token lives in git config on disk.
Any later process in the job can read that token.
This risk grows with pull_request_target jobs.
Upstream issue 485 reports this token leak.
GitHub Security Lab reports the same risk.
ArtiPACKED research found leaked tokens in artifacts.

## Decision

This action defaults persist-credentials to false.
This is the only default that differs from upstream.
All other inputs and defaults match upstream exactly.
Users can set persist-credentials to true when they need it.

## Consequences

Git config holds no token after checkout.
Later git push, fetch, and pull fail closed.
Later submodule update and LFS pull fail.
Private clones after checkout fail.
Release tools that need git write fail.
Users must use a separate push job with persist true.
The gh CLI still works in the job.
False does not hide the token from job steps.
Token power comes from the permissions block, not from persist.

## Rejected alternatives

Upstream default true: keeps the token on disk by default.
No wrapper action: users must repeat persist false in every job.
