# WebJET CMS skills

WebJET CMS development skills and architecture references for Codex, GitHub Copilot and Claude Code, including customer projects created from older basecms templates.

This repository is a generated distribution. **Edit skills and submit pull requests in [webjetcms/webjetcms](https://github.com/webjetcms/webjetcms)**: skills live in `.agents/skills`, shared knowledge in `.github/agents`. Direct edits to this distribution are replaced by the next export. `source.json` records the source commit and content hash. Original license information and skill attribution are retained; see [LICENSE.md](LICENSE.md) and each skill's metadata.

## Install

Installation uses the existing [skills CLI](https://github.com/vercel-labs/skills). Install Node.js 22.20 or newer, npm and Git. The tested installer version is `skills@1.7.2`. A newer installer may have different runtime requirements.

Run in the customer project's root, and select the agents to use:

```sh
npx skills@latest add webjetcms/skills --skill '*'
```

For a personal installation available across projects:

```sh
npx skills@latest add webjetcms/skills --skill '*' --global
```

For unattended installation, select the target agents explicitly:

```sh
npx --yes skills@latest add webjetcms/skills --skill '*' --agent codex github-copilot claude-code --yes
```

Add `--copy` when you want independent copies instead of symlinks, for example on Windows without symlink support. Skills are placed in the agent's recognized directories; npm is only used to run the installer. No CMS dependency or project `package.json` needs to change.

To install only the datatable workflow and its setup/context companions:

```sh
npx skills@latest add webjetcms/skills --skill wj-datatable wj-codeceptjs wj-project-context wj-setup
```

The installer does not resolve dependencies between skills. Include the companions a selected workflow requires. Existing skills can be overwritten: see the migration instructions below before replacing manual copies.

## Connect project instructions

After installation, ask your agent:

> Use wj-setup to connect the installed WebJET CMS skills to this project's instructions. Preserve the project's existing rules.

Installation alone does not execute this step. Setup adds managed blocks to the project instruction files for the three supported agents, including an existing root `AGENTS.override.md`. It preserves other content. Local context links are relative; global installations refer to the installed skill by name. Global instruction files are never changed.

For a local installation, the equivalent command is:

```sh
node .agents/skills/wj-setup/scripts/setup-project.mjs --project . --scope project
```

For global installations, let the agent locate the installed `wj-setup` script and pass `--scope global` with the customer project directory. Add `--dry-run` to preview. Keep custom rules outside `<!-- webjet-skills:start -->` and `<!-- webjet-skills:end -->`. If markers are damaged, repair them before rerunning; setup does not guess which user text to replace. Symlinked instruction files need manual integration.

For a single request that covers installation and setup, paste this into your coding agent:

> Install all official WebJET CMS skills from https://github.com/webjetcms/skills into this project using npx skills. Target the coding agent I am currently using. Before replacing existing skills, preserve and compare any manual copies. Then use wj-setup to connect wj-project-context to this project's instructions without replacing my custom rules. Do not update WebJET CMS or basecms.

For personal installation, replace "into this project" with "globally for my user; then configure this project's instructions". The agent needs terminal access, network access and permission to write the chosen directories. Giving the source URL avoids relying on search by an ambiguous name.

## Use and compatibility

Ask for a WebJET task, or name a skill explicitly, for example `wj-datatable`. The host can choose a skill by its description. Start a new session if changed persistent instructions have not been loaded.

One maintained skill set serves core and customer projects. Skills inspect the installed CMS version, available APIs and project conventions. They do not guarantee that a new framework feature exists in every historical CMS version. They do not upgrade CMS, create missing test infrastructure or install external plugins automatically. Specialized workflows, such as feature videos, require their documented tools and helpers.

Project rules take precedence over shared defaults. Framework source paths are reference locations, not a requirement to copy the CMS source into a customer project.

## Update and pin

Use the installer's interactive update command to select the intended scope:

```sh
npx skills@latest update
```

To update selected WebJET skills without updating unrelated skills:

```sh
npx skills@latest update wj-project-context wj-setup wj-datatable wj-codeceptjs --project
```

Use `--global` for global updates. Re-run `wj-setup` after updating it. The installer updates skill folders, while setup updates only its marked instruction blocks. Keep local customizations in project instructions or separately named skills. Do not expect the installer to merge edits inside installed WebJET skills.

For a reproducible installation, replace `DISTRIBUTION_COMMIT_SHA` with the full commit SHA from **this distribution repository**, not the source CMS revision in `source.json`:

```sh
npx skills@1.7.2 add https://github.com/webjetcms/skills/tree/DISTRIBUTION_COMMIT_SHA/skills --skill '*'
```

Retain the installer's project lock file and installed files according to your team's policy. For a pinned deployment, change the selected revision explicitly and verify it; do not use an unqualified update as a release policy.

## Migrate manual copies

1. Inspect existing `wj-*` folders in both project and global skill directories. Back up any local changes outside the installation destinations.
2. Compare them with the distribution. Move customer-specific rules into the project's instructions or a separately named skill before replacement.
3. Install in the chosen scope and verify the skill catalog. Remove obsolete duplicates only after comparing them; project and global copies can otherwise both appear.
4. Run `wj-setup` and review its diff. It does not remove old hand-written references to `.github/agents`; reconcile those manually if they conflict with the new context.

To remove the integration, use `npx skills remove` for the selected WebJET skills and remove only the marked WebJET blocks from project instruction files. Keep unrelated project instructions.

## Skill catalog

The following catalog and example prompts come from the English [WebJET usage guide](https://github.com/webjetcms/webjetcms/blob/4588dbc7965fe08bcb231e1d1c9125a9f08865c8/docs/en/developer/guidelines/ai-skills.md#webjet-skills-overview). Copy a prompt into your agent's chat and replace the bracketed placeholders. Skill names link to their full instructions and prerequisites. Only skills included in this distribution are listed.

<!-- webjet-skills-catalog:start -->
| Skill | What is it for and when to use it? | Example of entry into the chat |
| --- | --- | --- |
| [`wj-accessibility`](skills/wj-accessibility/SKILL.md) | Checks and improves web accessibility according to WCAG 2.2, such as keyboard controls, element descriptions, and screen reader support. | Use the wj-accessibility skill to check the accessibility of the form [URL]. |
| [`wj-add-javadoc`](skills/wj-add-javadoc/SKILL.md) | It adds and corrects the English JavaDoc of classes and methods, including parameters, return values, and exceptions. It only changes comments. | Use the skill wj-add-javadoc for class [path to Java file]. |
| [`wj-add-jsdoc`](skills/wj-add-jsdoc/SKILL.md) | It completes and checks English JSDoc in JavaScript according to the actual behavior of functions and their interface. It only changes comments. | Use the wj-add-jsdoc skill for JavaScript files changed in this branch. |
| [`wj-add-junit-comments`](skills/wj-add-junit-comments/SKILL.md) | It documents in English what JUnit test classes and methods verify. It does not change the behavior of the tests. | Use the skill wj-add-junit-comments for test [path to Java file]. |
| [`wj-anti-slop`](skills/wj-anti-slop/SKILL.md) | It refines the Slovak documentation, removes fluff, and explains functions through user tasks. It preserves technical meaning. | Use the wj-anti-slop skill for documentation [path to Markdown file]. |
| [`wj-appstore-app`](skills/wj-appstore-app/SKILL.md) | It creates applications embedded in pages via the AppStore, including Spring MVC components, Thymeleaf views, and editor parameters. | Use the wj-appstore-app skill to create an application [description and parameters]. |
| [`wj-code-review`](skills/wj-code-review/SKILL.md) | It checks the correctness of changes, backward compatibility, and code quality before committing or merging a PR. | Use the wj-code-review skill for uncommitted changes to the [issue description or URL] task. |
| [`wj-codeceptjs`](skills/wj-codeceptjs/SKILL.md) | Writes and edits E2E tests via CodeceptJS and Playwright with existing WebJET CMS helper functions. | Use the wj-codeceptjs skill to test creating, editing, and deleting a record in [application]. |
| [`wj-codeceptjs-check`](skills/wj-codeceptjs-check/SKILL.md) | Finds and reruns existing tests based on the list of failures from Allure. This is used to verify the fix; it does not change the tests. | Use the wj-codeceptjs-check skill for these failures from Allure on [environment URL]: [list]. |
| [`wj-confirm-issue`](skills/wj-confirm-issue/SKILL.md) | Will review a specific code review finding or reported issue and propose a solution for approval before implementation. | Use the wj-confirm-issue skill to verify this finding: [finding and file]. |
| [`wj-content-marketing`](skills/wj-content-marketing/SKILL.md) | From Git changes, it suggests topics and content for blogs, social posts, emails, or press releases about delivered features. | Use the wj-content-marketing skill and suggest blog topics from the changes in [commit range]. |
| [`wj-create-feature-video`](skills/wj-create-feature-video/SKILL.md) | Prepares a product video from PR or branch: script, localized commentary, recordings, and editing with WebJET conclusion. Requires tools and approaches listed in the skill, including ElevenLabs and Tesseract. | Use the skill wj-create-feature-video for PR [URL], language Slovak, target group editors. |
| [`wj-dashboard-widget`](skills/wj-dashboard-widget/SKILL.md) | Creates and edits admin home screen widgets, including data, settings, permissions, and responsive variants. | Use the wj-dashboard-widget skill to create a widget [data, settings, and permissions]. |
| [`wj-datatable`](skills/wj-datatable/SKILL.md) | Creates and modifies administrative CRUD applications: JPA entity, repository, REST controller, DataTable page, and tests. | Use the wj-datatable skill to create a record [fields, rules, and permissions]. |
| [`wj-dependencycheck`](skills/wj-dependencycheck/SKILL.md) | Evaluates OWASP Dependency Check findings based on severity and usability in WebJET CMS. Submits a proposal for decision before changing dependencies or exceptions. | Use the wj-dependencycheck skill on report [path], handle severities HIGH and CRITICAL. |
| [`wj-docs-pr`](skills/wj-docs-pr/SKILL.md) | Updates the selected Markdown document according to all relevant changes in the PR or according to local changes. | Use the wj-docs-pr skill to update [document path] according to PR [URL]. |
| [`wj-gh-issue-from-chat`](skills/wj-gh-issue-from-chat/SKILL.md) | Creates a draft of a new GitHub issue from the discussion, decisions, and plan, saves it after confirmation, and suggests a branch name. It does not create a branch. | Use the skill wj-gh-issue-from-chat and prepare an issue from the agreed assignment in this chat. |
| [`wj-gh-issue-from-grill`](skills/wj-gh-issue-from-grill/SKILL.md) | It transfers the agreed conclusions of the discussion into an existing issue, including criteria, plan, and tests. It does not create a new issue or start implementation. | Use the skill wj-gh-issue-from-grill for issue [URL] and incorporate the agreed conclusions of this chat. |
| [`wj-page-builder`](skills/wj-page-builder/SKILL.md) | Creates and edits PageBuilder HTML blocks, including nesting, editable areas, columns, and duplicatable elements. | Use the wj-page-builder skill to create a reference block with three columns and duplicable items. |
| [`wj-project-context`](skills/wj-project-context/SKILL.md) | It loads the WebJET CMS architecture and conventions and verifies their applicability for a specific core version or customer project. | Use the skill wj-project-context and over to correctly read the configuration and translations in this project. |
| [`wj-sales-features`](skills/wj-sales-features/SKILL.md) | Prepares a Slovak business description of functions from the PR, branch or annexes: benefits, advantages and value for the customer. | Use the wj-sales-features skill for PR [URL] and describe the benefits for the customer. |
| [`wj-setup`](skills/wj-setup/SKILL.md) | Once installed, WebJET skills will connect to project guidelines for Codex, GitHub Copilot, and Claude Code. It will retain your own project rules. | Use the wj-setup skill to link the installed WebJET skills to this project. |
| [`wj-simplify-implementation`](skills/wj-simplify-implementation/SKILL.md) | It simplifies implementation in PR or local changes and removes unnecessary complexity while preserving behavior. | Use the wj-simplify-implementation skill for uncommitted changes to this feature. |
| [`wj-stylescombo`](skills/wj-stylescombo/SKILL.md) | Adds or restores style metadata in editor.css or editor.scss: names, categories, groups, and constraints according to the full template styles. | Use the skill wj-stylescombo: add missing metadata in [editor.scss], complete styles are in [ninja.scss], language Slovak. |
| [`wj-translate-comments`](skills/wj-translate-comments/SKILL.md) | Translates Slovak comments in code into English without changing the logic or texts of the application. | Use the wj-translate-comments skill only on comments in [file or folder]. |
| [`wj-ui-review`](skills/wj-ui-review/SKILL.md) | It checks the existing interface, its layout, typography, colors and interactions against WebJET CMS conventions. It makes specific visual corrections upon request. | Use the wj-ui-review skill on the [URL or screenshot] screen and list the findings without editing. |
<!-- webjet-skills-catalog:end -->
