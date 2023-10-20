# gh-squash-merge

I use squash merge a lot when messing around with pull requests. One of the things that has irked me is the _manual love_ that we need to sometimes apply when doing the commit message on merge. If you do not have structured commit messages and it's multiple commits you want to squash merge, then you effectively have to stop and think at the point of merge. Thinking can be hard; I don't like hard, and this kind of problem seems like toil that can be automated away.

You need to have some kind of discipline in place in order to seamlessly 'just use an aggregation of all your commit messages on that PR branch'. I'm all for discipline but perhaps along the journey of your development you've actually changed your mind a couple of times, and text you write _in the PR body_ is actually more meaningful than the commit messages you've written previously.

This is an extension for [GitHub CLI](https://cli.github.com/) that just parses your PR body for some meaningful text and uses that as the commit message when you squash merge.

## Installation

- [GitHub CLI](https://cli.github.com/) is already installed and authenticated
- awk is available, untested with awk on MacOS; but I don't think I'm doing anything _special_ in awk...
- mktemp is available, untested with mktemp on MacOS; but `--tmpdir` isn't that special right?
- `gh extension install quotidian-ennui/gh-squash-merge`

## Setup

You probably want to have a `pull_request_template.md` available in your repo / organisation that looks something like this; it should be self-explanatory what the boundary markers are and what the point of them are...

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
Usage: gh squash-merge [--keep-branch] <pr-number>

Issues a squash merge on the PR number provided.

Required arguments
  <pr-number> The PR number to squash merge

Optional arguments
  --keep-branch  Do not delete the branch after merge
                 default is to delete the branch.

Notes:
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
