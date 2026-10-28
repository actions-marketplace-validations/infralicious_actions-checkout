# Architecture Decision Records

Decisions that are hard to reverse, or touch security, live here.
Small changes need no ADR.
UI copy and refactors need no ADR.

## Format

Each record is one file: `NNNN-short-title.md`. Numbers never change.
Each record holds: status, date, context, decision, consequences, rejected alternatives.
Keep each record to one page.

## Process

An ADR ships in the same commit as its decision.
A superseding ADR links the old record, and the old record is marked superseded.
Living docs link to the ADR number.
Living docs do not copy full reasoning again.

## Index

- 0001: Persist-credentials defaults to false (Accepted)
- 0002: Exact tag only, no floating major tag (Accepted)
- 0003: Upstream pin uses full SHA with version comment (Accepted)
- 0004: No backfill, fill only newer releases (Accepted)
- 0005: Human review stays, no full automation (Accepted)
