# Checkout without persisted credentials

[![OpenSSF Scorecard](https://api.securityscorecards.dev/projects/github.com/infralicious/actions-checkout/badge)](https://securityscorecards.dev/viewer/?uri=github.com/infralicious/actions-checkout)

This action passes through to `actions/checkout`.
It uses the full upstream SHA, not a moving tag.
It keeps every upstream input and default.
Only `persist-credentials` changes.
It defaults to `false`, not `true`.

## Why this repo exists

Upstream keeps true as default for push convenience.
Upstream has not changed that default.
[Issue 485](https://github.com/actions/checkout/issues/485) asked for a change in 2021.
Upstream still uses true today.
This repo wraps upstream.
It does not copy upstream code.
It gives users a secure default without a fork.

## What problem it solves

Many workflows use checkout in many places.
One missed setting leaks a token.
Later code in the same job can then use that token.
That code can include untrusted code from a fork.
Upstream default stores a token for later git use.
[Issue 485](https://github.com/actions/checkout/issues/485) calls this a severe security issue.
[GitHub Security Lab](https://securitylab.github.com/resources/github-actions-preventing-pwn-requests/) links this default to pwn requests.
[ArtiPACKED research](https://dev.to/rxkov/github-actions-when-the-cicd-pipeline-becomes-a-secrets-exfiltration-vector-pea) found tokens in uploaded artifacts in 2024.
Older versions stored the token in `.git/config` directly.
Newer versions store it in a temp file instead.
Later steps can still use that temp file for git.
Current version keeps that temp file design.
False removes that later use by default.
This repo removes that miss by default.
You do not need to repeat the setting.
False does not fix all token risks.

## Switch from upstream

Use this diff to switch from upstream.
You remove the with block in both forms.
Diff shows step lines, not a patch file.

Tag form:

```diff
- uses: actions/checkout@v7.0.1
-   with:
-     persist-credentials: false
+ uses: infralicious/actions-checkout@v7.0.1
```

SHA form:

```diff
- uses: actions/checkout@3d3c42e5aac5ba805825da76410c181273ba90b1 # v7.0.1
-   with:
-     persist-credentials: false
+ uses: infralicious/actions-checkout@c9b2547edbff66d33a1c6b175ea258c8d10c6689 # v7.0.1
```

Tag in this repo pins upstream SHA internally.
Our SHA for v7.0.1 is c9b2547edbff66d33a1c6b175ea258c8d10c6689.
Use that SHA for full SHA pinning.
Use commit SHA, not tag object SHA.

## Use

```yaml
- uses: infralicious/actions-checkout@v7.0.1
```

Use this form to pass an input:

```yaml
- uses: infralicious/actions-checkout@v7.0.1
  with:
    fetch-depth: 0
```

You may omit `repository` and `token`.
The action then uses the workflow repository and token.
Composite defaults cannot evaluate workflow values directly.
The step adds that fallback at run time.
You may set `persist-credentials` to `true` when you need it.
With `false`, later steps cannot push with the stored token.
Configure git credentials yourself for a later push.

## Outputs

It returns `ref` from upstream.
It returns `commit` from upstream.

## Upstream pin

Upstream version is v7.0.1.
Upstream SHA is `3d3c42e5aac5ba805825da76410c181273ba90b1`.
This repo tag is v7.0.1.
This repo SHA is `c9b2547edbff66d33a1c6b175ea258c8d10c6689`.
Use exact version tag only, not floating major tag.
A floating major tag does not exist in this repo.

## Inputs

Inputs match upstream exactly, except one change.
`persist-credentials` defaults to `false`.
See `action.yml` for the full input list.

## Limits

This action does not remove tokens from other steps.
It does not scan artifacts for tokens.
Use least privilege permissions in each job.
This repo does not support upstream versions older than the current tag.

See [CONTRIBUTING](CONTRIBUTING.md) for maintainer steps.
