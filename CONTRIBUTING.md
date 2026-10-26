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
Renovate updates code SHA lines and README version lines.
Renovate groups those updates in one PR.
Review the PR for input changes.
Upstream-check fails if inputs change.
Add input changes to the PR when it fails.
Set persist-credentials default to false only.
Change no other input default.
Update README upstream SHA line from the PR diff.
Merge the PR when tests pass.
Create a new repo tag that matches upstream tag.
Update README repo SHA after tag creation.
Update README SHA diff after tag creation.
Renovate cannot create a tag.
Renovate cannot know repo SHA before tag exists.
Manual fallback follows if Renovate misses an update.
Read the upstream-check failure log for the new tag name.
Fetch upstream action.yml for the new tag.
Copy all inputs from upstream to local action.yml.
Set persist-credentials default to false only.
Change no other input default.
Update the upstream pin SHA to the new tag SHA.
Update README version and SHA to the new values.
Create a new repo tag that matches upstream tag.
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
Publish needs the Marketplace Developer Agreement.
Publish needs a primary category.
Publish needs two factor authentication.
Org owner must accept the agreement.
Name must be unique on the Marketplace.

## Major tag

No floating major tag exists in this repo.
Use exact version tag only, not a floating major tag.
A floating major tag would move on each release.
A moving tag breaks SHA pinning for users.
If a major tag is ever added, move it after each new version tag.
Move it with a signed tag and a force push.
A workflow move would not be SSH signed.
