# Plan: spook-fixes-1

## What Sean asked for
"Do #2096": fix the broken documentation links in spook and send the fix to the original project (frenck/spook) as its own pull request.

## What we found
- **Only one open issue is worth fixing now.** Of spook's 32 open issues, every other real bug already has a pull request from someone else. The rest are reports nobody could reproduce, already fixed, or waiting on the maintainer.
- **The broken links (#2096):** 35 "documentation" links on the Triggers (23), Conditions (9) and Actions (3) pages point to `other-features#...`, but the page's file is `other_features.md`. The site leaves them as plain links, so each one opens a "page not found" error, for example `https://spook.boo/triggers/other-features`.
- **The right form already works elsewhere:** the Features page links to `(other_features)` and the live site turns that into a working link. Links to other pages, like `areas#create-an-area`, use the file name the same way.
- **The fork's main branch matches the original project.**

## What we'll change
1. **Fix the links** in `documentation/triggers.md`, `documentation/conditions.md` and `documentation/actions.md`: change each `](other-features#` to `](other_features#`. Nothing else in those files changes.
   - **Check:** no `other-features#` links remain, and the count of changed links is 35.
2. **Build the documentation site** the way the project's own check does (`myst build --html` in `documentation/`).
   - **Check:** the built pages link to the working `other-features` page and anchors, with no links to `triggers/other-features`, `conditions/other-features` or `actions/other-features`. Spot-check that a few of the anchors (for example "Automation turned off" and "Cron schedule") exist on the Other features page.
3. **Run the project's checks** that apply: the docs build, prettier on the changed files, and the full test suite to show nothing else changed.
4. **Send upstream, only after the final approval on this PR:**
   - One clean branch from the original project's latest code, holding only this fix. The plan file never goes upstream.
   - One pull request to frenck/spook, from Sean's account, using the project's pull request template. It's written as Sean working alone, with "Fixes #2096".
   - Draft title: "Fix broken links to the Other features page".
   - The full title and description are shown here first.

## Who's on it
Engineer, Security Officer and Auditor. This is a small docs-only change, so there's no separate research step beyond what's above, and no plan check or QA step: the Engineer runs the checks and the Auditor checks them.

## Risks
- **Link form:** the main risk is that the site builder handles `other_features#anchor` differently from bare `other_features`. The docs build in step 2 checks this before anything is sent.
- **The maintainer may fix it first:** the issue was opened on 2026-11-18, and he often fixes things within days. If he does, we close ours.

## Out of scope
- Other spook issues: they have open pull requests from others, or need the maintainer.
- Any other docs wording, and the project's own tooling files.
- Fork-only files: no guidelines file, badges or notes go into the upstream pull request.
