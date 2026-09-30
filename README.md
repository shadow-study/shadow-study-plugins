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

## Exam-player configuration

`mcp.json` uses the portable Agent Plugins remote HTTP configuration described in
[OpenAI's packaging guide](https://developers.openai.com/plugins/build/plugins), checked September
30, 2026. It points to the hosted service; it bundles no server or player source.

`player-contract.json` is developer validation data, not a provider manifest or an OAuth client.
It records the hosted resource/tool contract and the explicit practice permission the connection
must request: `exams:import study:practice`. Results access is a separate optional permission.
The learner approves practice through Shadow Study's existing delegated consent flow; installing
this endpoint configuration alone does not grant practice or change an existing connection.
The provider-specific setup that requests this permission still needs real-client testing.

The player is experimental and disabled by default on the hosted service. It covers starting or
resuming one exam, saving choices, checking Study answers, submitting and viewing that attempt.
History, Dashboard, library management, account and billing remain on shadow.study. Practice works
with AI result sharing turned off, and the player does not deliberately send answers or results to
the chat model. Every protected operation requires current Shadow Study access.

In an initialized application worktree, run `bash scripts/check-player-config.sh plugin` before
updating the submodule pin. The command checks this configuration against a disposable local Rust
server and a synthetic UI host; it never probes the production endpoint. Record the tested parent
and package commits and result in the parent PR. Full release preparation and publication remain
under application issue #45; this configuration is not a store submission.
