# Checkout, without persisted credentials by default

This action passes through to `actions/checkout` v7.0.1.
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
Version 6 and later store it in a temp file instead.
Later steps can still use that temp file for git.
Version 7 keeps that temp file design.
False removes that later use by default.
This repo removes that miss by default.
You do not need to repeat the setting.
You still can set it true when needed.
False does not fix all token risks.
Scope tokens to read only when you can.
Pass a token only to steps that need it.

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
+ uses: infralicious/actions-checkout@v7.0.1
```

Tag v7.0.1 in this repo pins upstream SHA internally.
Full SHA form for this repo needs its commit SHA.
That SHA exists only after the first push.
Update this doc with that SHA after push.

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
Use v7.0.1 only, not v7.
A v7 tag does not exist in this repo.
Update this tag when upstream releases a new version.
Match the new tag to the new upstream version.

## Update to a new upstream version

Upstream-check workflow fails when upstream releases a new tag.
Read the failure log for the new tag name.
Fetch upstream action.yml for the new tag.
Copy all inputs from upstream to local action.yml.
Set persist-credentials default to false only.
Change no other input default.
Update the upstream pin SHA to the new tag SHA.
Update README version and SHA to the new values.
Create a new repo tag that matches upstream tag.
Run the test workflow and check it passes.
Upstream-check workflow also checks inputs on each run.
It fails if any default differs except persist-credentials.
It fails if an input is added, removed, or renamed.
It prints the exact input diff in the log.
A human must apply that diff by hand.
Automation never changes a default by itself.

## Inputs

Inputs match upstream v7.0.1 exactly, except one change.
`persist-credentials` defaults to `false`.
See `action.yml` for the full input list.

## Limits

This action does not remove tokens from other steps.
It does not scan artifacts for tokens.
Use least privilege permissions in each job.
