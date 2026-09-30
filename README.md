# Shadow Study plugins

Plugin packages and store submission assets for the hosted [Shadow Study](https://shadow.study)
service, initially for ChatGPT and any later approved Claude package.

This repository is private during preparation. It will receive its own open-source license before
public release. Store-ready manifests, listing assets, and release validation are still to be built;
this initial commit establishes the package workspace only.

## Package boundary

This repository may contain reviewed plugin manifests, remote MCP configuration, branding and
listing assets, setup/support documentation, and deliberately approved minimal workflow skills.
The hosted MCP endpoint is `https://shadow.study/mcp`.

The application backend, OAuth implementation, grading, database logic, website, and exam-player
source remain in the private application repository. Protected prompts, samples, exam schemas,
generated resources, credentials, learner content, and private deployment configuration belong
outside this repository. Do not use file symlinks or imports into application files when preparing a
release. Compiled exam-player assets are served by the hosted application.

Package installation uses the learner's linked Shadow Study account, delegated permissions, and
current study entitlement; publishing a package does not provide study access.

## Development

The application repository links this repository at `plugin/` as a Git submodule. This repository
has independent history; commit package changes here and push them before updating the pinned
package commit in the application repository. Create a package branch before editing a submodule
checkout that is on a detached HEAD. Application CI and builds do not need this private submodule
initialized.

Keep this initial workspace independent of the application build. Add provider-specific package
files and release checks through the approved package work, and review all tracked files before
changing visibility or publishing a release.
