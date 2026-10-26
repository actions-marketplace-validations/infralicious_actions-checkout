# Contributing

This file is for maintainers.
It covers repo workflows and upstream updates.

## Repo workflows

Repo workflows use upstream for setup only.
Test steps use ./ for our wrapper.
Setup needs repo files before ./ can run.
Published wrapper would test old tag, not local code.
Published wrapper failure would block local test.
Upstream setup keeps local test independent.
Upstream-check setup keeps the check independent.
Check compares wrapper against upstream oracle.

## Update to a new upstream version

Renovate opens a PR when upstream releases a new tag.
Renovate updates code SHA lines only.
README has no version lines and no SHAs.
README needs no update for a new version.
Review the PR for input changes.
Upstream-check fails if inputs change.
Add input changes to the PR when it fails.
Set persist-credentials default to false only.
Change no other input default.
Merge the PR when tests pass.
Create a new signed repo tag that matches upstream tag.
Create a GitHub Release for that tag.
Release notes must link to the upstream release.
Release notes must use the upstream release URL for that tag.
Renovate cannot create a tag.
Renovate cannot create a release.
Manual fallback follows if Renovate misses an update.
Read the upstream-check failure log for the new tag name.
Fetch upstream action.yml for the new tag.
Copy all inputs from upstream to local action.yml.
Set persist-credentials default to false only.
Change no other input default.
Update the upstream pin SHA to the new tag SHA.
Keep the version comment on the pin line.
Create a new signed repo tag that matches upstream tag.
Create a GitHub Release for that tag.
Release notes must link to the upstream release.
Run the test workflow and check it passes.
Upstream-check also checks inputs on each run.
It fails if any default differs except persist-credentials.
It fails if an input is added, removed, or renamed.
It prints the exact input diff in the log.
A human must apply that diff by hand.
Automation never changes a default by itself.

## Marketplace publish

Action is not published on the Marketplace yet.
Action works without a Marketplace listing.
Users can use the repo tag directly.
Publish needs branding in action.yml.
Publish needs a GitHub Release for the tag.
Publish needs a signed tag for the tag.
Publish needs the Marketplace Developer Agreement.
Publish needs a primary category.
Publish needs two factor authentication.
Org owner must accept the agreement.
Name must be unique on the Marketplace.

## Major tag

No floating major tag exists in this repo.
Do not add a floating major tag.
Use exact version tag only.
Floating tag must move on each release.
Immutable release locks its tag to one commit.
Floating tag and immutable release cannot both work.
Exact tag only keeps releases immutable.

## Releases

Sign every tag with SSH signing.
Create a Release for every tag.
Release must be immutable.
Verify the release with gh release verify.
Release notes must link to the upstream release.
Release notes must not hardcode SHAs.
Use placeholders in README, not in release notes links.
Upstream release URL uses the upstream tag name.

## Immutable releases

Immutable releases are enabled at repo level.
Settings file cannot enable immutable releases.
Enable it with gh api PUT for immutable releases.
Future releases will be immutable automatically.
Do not move a tag after its release is created.
Tag cannot move, delete, or reuse after release.
Do not delete an immutable release to reuse its tag.
Deleted immutable tag name cannot be reused.
Verify a release with gh release verify for its tag.
