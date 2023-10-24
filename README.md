# gh-squash-merge

I use squash merge a lot when messing around with pull requests. One of the things that has irked me is the _manual love_ that we need to sometimes apply when doing the commit message on merge. If you do not have structured commit messages and it's multiple commits you want to squash merge, then you effectively have to stop and think at the point of merge. Thinking can be hard; I don't like hard, and this kind of problem seems like toil that can be automated away.

You need to have some kind of discipline in place in order to seamlessly 'just use an aggregation of all your commit messages on that PR branch'. I'm all for discipline but perhaps along the journey of your development you've actually changed your mind a couple of times, and text you write _in the PR body_ is actually more meaningful than the commit messages you've written previously.

This is an extension for [GitHub CLI](https://cli.github.com/) that just parses your PR body for some meaningful text and uses that as the commit message when you squash merge.

## Installation

- [GitHub CLI](https://cli.github.com/) is already installed and authenticated
- `awk` is available, untested with awk on MacOS; but I don't think I'm doing anything _special_ in `awk`...
- `mktemp` is available, untested with `mktemp` on MacOS; but `--tmpdir` isn't that special right?
- `gh extension install quotidian-ennui/gh-squash-merge`

## Setup

You probably want to have a `pull_request_template.md` available in your repo / organisation that looks something like this; it should be self-explanatory what the boundary markers are and what the point of them are...

```markdown
# Motivation
<!-- Why am I doing this -->

## Changes

<!-- Bits between these two tags can be used as the squash_merge_commit_message when the PR is
     approved and merged -->
<!-- SQUASH_MERGE_START -->

<!-- SQUASH_MERGE_END -->
```

- Any text that you write between the `SQUASH_MERGE_START` & `SQUASH_MERGE_END` will be used as the commit message.

### Usage

```text
Usage: gh squash-merge [<number> | <url> | <branch>] [flags]

Issues a squash merge on the PR.

Without an argument, the pull request that belongs to the current branch
is used.

Arguments
  <number> The PR number to squash merge
  <url> The PR URL to squash merge
  <branch> The branch of PR URL to squash merge

Flags
  -R, --repo [HOST/]OWNER/REPO   Select another repository using the [HOST/]OWNER/REPO format

Notes:
- The title of the commit will be based on GitHub repository settings
- The PR body contains a section similar to the following which lets us autogenerate
  squash merge commit message
- If PR body does not contain a section similar an empty body will be set

<!-- SQUASH_MERGE_START -->
- this forms the body of the commit message and could be multiple lines
but generally we tend towards
- doc: conventional commit messages
<!-- SQUASH_MERGE_END -->

EXAMPLES
gh squash-merge
gh squash-merge 811
gh squash-merge --repo quotidian-ennui/gh-squash-merge 811
gh squash-merge https://github.com/quotidian-ennui/gh-squash-merge/pull/811
gh squash-merge feature/update
```

## License

See [LICENSE](./LICENSE)
