# gh-squash-merge
Squash+Merge a PR with a commit based on the PR body
# gh-my

We use squash merge a lot when messing around with pull requests. One of the things that has irked me is the _manual love_ that we need to sometimes apply when doing the commit message on merge. If you do not have structured commit messages and it's multiple commits you want to squash merge, then you effectively have to stop and think at the point of merge.

You actually need to have some kind of discipline in place in order to seamlessly 'just use an aggregation of all your commit messages on that PR branch'; I'm all for discipline, but this is a case

This is an extension for [GitHub CLI](https://cli.github.com/) that just parses your PR body for some meaningful text and uses that as the commit message when you squash merge.


## Installation

- [GitHub CLI](https://cli.github.com/) is already installed and authenticated
- awk is available, untested with awk on MacOS; but I don't think I'm doing anything _special_ in awk...
- Just `gh extension install quotidian-ennui/gh-squash-merge`

## Setup

You probably want to have a `pull_request_template.md` available in your repo / organisation that looks something like this; it should be self-explanatory why the boundary markers are there.

```
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

```
Usage: gh squash-merge <pr-number>

Issues a squash merge on the PR number provided.

- The title of the commit is the title of the PR
- The PR body contains a section similar to the following which lets us autogenerate
  squash merge commit message

<!-- SQUASH_MERGE_START -->
- this forms the body of the commit message and could be multiple lines
but generally we tend towards
- doc: conventional commit messages
<!-- SQUASH_MERGE_END -->

EXAMPLES
gh squash-merge 811
```


## License

See [LICENSE](./LICENSE)
