# AGENTS.md — actions-checkout

Instructions for AI agents working in this repo.
Claude Code reads these through CLAUDE.md (`@AGENTS.md`).

## What this repo is

- Composite action, not a copy of upstream code.
- Action passes every input through to upstream checkout.
- Action pins upstream by full SHA, not a moving tag.
- Only `persist-credentials` default differs from upstream.
- Local default is false, upstream default is true.
- Repo tag matches upstream tag exactly.
- No floating major tag exists in this repo.
- Floating tag cannot move after an immutable release.
- Immutable release locks its tag to one commit.
- Immutable releases are enabled at repo level via gh cli.
- Settings file cannot enable immutable releases.
- SHA pinning is enforced at repo level via Actions permissions.
- Settings file cannot set SHA pinning.
- Enable it with gh api PUT for Actions permissions.
- Tag ruleset protects v star tags.
- Settings file cannot set tag ruleset.
- Ruleset blocks tag deletion, update, and non fast forward.
- Ruleset has no bypass actors.
- Disable ruleset first to move a tag, then re-enable it.
- Sign every tag with SSH signing.
- Create a Release for every tag.
- Release notes must link to the upstream release.
- Verify a release with gh release verify.
- Do not delete an immutable release to reuse its tag.
- Old upstream versions get no support.
- Tag stays at its commit after it ships.
- Main changes do not move a shipped tag.
- New tag ships only with a new upstream tag.

## Language rule

- Write everything in ASD-STE100 Simplified Technical English.
- Short sentences (max 20 words). Active voice. One idea per sentence.
- No idioms, slang, or complex words. No em dashes. Use hyphens or restructure.

## Hardcoded versions and SHAs

- Do not hardcode a SHA in README.
- Use <upstream-sha> and <repo-sha> placeholders in README.
- Keep a SHA in code lines that pin an action.
- Keep a version comment on a code SHA line.
- Remove a version from descriptions, intros, and prose comments.
- Generalize a comment when a version would go stale.
- Repo description must not mention an exact version.
- Version comment on a code SHA line is an exception.
- Renovate needs that comment to find the tag for a SHA.

## Renovate

- Renovate owns action SHA bumps.
- Renovate config lives in renovate.json5.
- Renovate runs before 3am on Monday.
- Renovate groups GitHub Actions updates in one PR.
- Renovate updates code SHA lines only.
- README has no version lines and no SHAs.
- Version comment on a SHA line is essential for Renovate.
- Renovate cannot update a SHA without a version comment.
- Keep version comment on every SHA pin line.
- This rule overrides the no hardcoded version rule for code lines.
- Renovate cannot create a repo tag.
- Renovate cannot create a release.
- Human still creates the tag after merge.
- Human still creates the release after tag.
- Upstream-check still catches input changes.
- Human adds input changes to the Renovate PR when needed.

## Commits and pushes

- Sign every commit (SSH signing is configured repo-local).
- Confirm before pushing, unless the user has told you to push freely.
- Push pattern: `git -c credential.helper='!gh auth git-credential' push origin main`.
- Small, topical commits. One change per commit.
- After a push, check the Test workflow run and report the result.

## Workflows

- Test workflow runs on push to main.
- Upstream-check workflow runs weekly and on manual dispatch.
- Scorecard workflow runs on push and weekly.
- Scorecard badge lives in README.
- Scorecard badge needs a published Scorecard run first.

## Automation

- Repo is not fully automated.
- Test, Upstream-check, Settings, Scorecard, and Renovate run automatically.
- Human still reviews and merges Renovate PRs.
- Human still creates signed tags.
- Human still pushes after approval.
- Full automation would need auto merge and auto tag.
- Auto tag would not be SSH signed by the user.
- Auto merge would ship upstream changes without review.
- Keep human review for this security action.

## Before you set persist false

- Check the job for git push, fetch, pull, submodule update, LFS pull, private clone, or release tool.
- If the job needs any of those, keep persist true or split the job.
- Do not set false in a push job.
- Use gh auth setup-git only in a push job.
- Read README Gotchas section before you change a workflow to false.

## Marketplace

- Action is not published on the Marketplace yet.
- Action works without a Marketplace listing.
- Publish needs branding, a release, agreement, and category.
- Publish needs two factor authentication.
- Org owner must accept the agreement.
- Name must be unique on the Marketplace.
- Current name is Checkout, which may not be unique.
- Test workflow setup uses upstream, not this wrapper.
- Local test steps use `./` for this wrapper.
- Upstream-check setup stays independent from this wrapper.
- Upstream-check compares every input against upstream.
- It fails if any default differs except `persist-credentials`.
- It fails if an input is added, removed, or renamed.
- A human must apply an upstream diff by hand.
- Automation never changes a default by itself.

## Repo settings as code

- `.github/settings.yml` is enforced by the Settings app. Change settings in that file, not in the GitHub UI.
- Main branch protection is on: no force push, no deletion. Direct pushes still work.
- No review or check gates are set on main.

## Do not touch

- Do not copy upstream code into this repo.
- Do not enter card details on the user's behalf.
- Do not publish an email address in this repo.
