# notedreamer

An agent plugin that looks back over a [Noteweaver](https://github.com/yiju-zhao/noteweaver)
knowledge bank and tidies what is already there. It adds no new material. It checks
pages and claims against the stored evidence, finds duplicates, stale values, broken
navigation and pages that grew without getting clearer, and turns corrections a
person made repeatedly in conversation into proposals.

The method follows the "dreaming" pass described in Anthropic's
[The components of agent memory](https://www.anthropic.com/research/components-of-agent-memory),
applied to a knowledge bank instead of an agent's own memory: the stored evidence
is the ground truth that written pages are checked against.

## What it does

One skill, `notedreamer`, with three scopes:

| Scope | Pages examined | When |
| --- | --- | --- |
| This conversation | Pages changed since a Git revision, plus their direct neighbours | After each write |
| One topic | Pages in a topic's scope, with its brief and run notes | After a few research runs |
| Whole bank | A sweep and a sample, not page by page | Periodically |

It fixes clear transcription errors, missing links and broken links directly.
Merges, renames, deletions, splits, conflicting values and policy changes are only
proposed; a person decides. Where the host can spawn a subagent, the check is done
by one that did not take part in the writing.

## Requirements

- A knowledge bank managed by Noteweaver, with the Noteweaver agent plugin installed
  on the same host. The topic scope needs a Noteweaver release that provides the
  `topic` operation (0.16.0 or later).
- The bank's own policies decide formats and where records go. This plugin holds
  the method only.

## Install

Claude Code:

```sh
claude plugin marketplace add yiju-zhao/notedreamer
claude plugin install notedreamer@notedreamer
```

For other hosts, point the host's plugin or skill discovery at this repository; the
skill is `skills/notedreamer/SKILL.md`.

## License

MIT
