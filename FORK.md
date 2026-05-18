# Samaluk Refined GitHub fork

This fork tracks upstream Refined GitHub and carries one personal feature that was not accepted upstream:

- `diff-stats-by-extension`: adds a clickable pull request diffstat popover that groups changed lines by file extension/type.

Preview: [`media/diff-stats-by-extension-preview.png`](media/diff-stats-by-extension-preview.png)

## Install locally

This fork is not published to browser extension stores. To try it, build and load the unpacked extension:

```bash
git clone https://github.com/samaluk/refined-github.git
cd refined-github
git checkout codex/diff-stats-by-extension
npm install
npm run build
```

Then load the `distribution/` directory as an unpacked extension:

- Chrome/Chromium: open `chrome://extensions`, enable **Developer mode**, choose **Load unpacked**, and select `distribution/`.
- Edge: open `edge://extensions`, enable **Developer mode**, choose **Load unpacked**, and select `distribution/`.
- Firefox: open `about:debugging#/runtime/this-firefox`, choose **Load Temporary Add-on**, and select `distribution/manifest.json`.

Because this is an unpacked/local build, browser updates will not update it automatically. Pull and rebuild when you want newer upstream changes.

## Keeping the fork in sync

Conservative manual sync process:

```bash
git remote add upstream https://github.com/refined-github/refined-github.git # once, if missing
git fetch upstream origin
git checkout codex/diff-stats-by-extension
git rebase upstream/main
npm run vitest -- build/features source/github-helpers/group-pr-files-by-extension.test.ts
npm run build
git push --force-with-lease origin codex/diff-stats-by-extension
```

If conflicts happen, resolve them during the rebase, rerun the commands above, then push with `--force-with-lease`.

## Upstream context

The upstream proposal was closed as out of scope/API-heavy for Refined GitHub proper:

- Issue: https://github.com/refined-github/refined-github/issues/9475
- Draft PR: https://github.com/refined-github/refined-github/pull/9476

This fork keeps the feature available for people who specifically want the PR-header summary despite those tradeoffs.
