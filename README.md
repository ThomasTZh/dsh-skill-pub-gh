# dsh-skill-pub-gh

This package holds short written instructions that help a person or an
assistant publish a project on a public code-sharing website. It decides what
may safely be shared, keeps proper credit for other people's work, and explains
the project in words a newcomer can follow. The instructions are one main file
plus two fill-in templates, and the result is checked before anything is
uploaded.

## Purpose and gaps

Releasing a project is not the same as uploading its working directory.

- **Gap:** a working copy carries credentials, local paths, logs, caches, and
  third-party code whose licence may not allow redistribution. Its README tends
  to describe a running machine rather than a reproducible one, and deciding
  what to publish, how to attribute it, and what can honestly be claimed is left
  to judgement. An overstated release is worse than no release.
- **Approach:** turn the task into a checked sequence: classify files, build an
  allowlist tree, pass privacy and licence gates, write the README from
  evidence, verify from a fresh directory, then push only after approval.

## Features

- **File classification and publication manifest:** records path, decision,
  class, origin, upstream version, licence, and reason for every candidate file
  before anything is copied.
- **Privacy and licence gates:** secret scanning, review of hidden files and
  image metadata, provenance and licence-compatibility checks, and a hard stop
  when ownership or obligations cannot be resolved.
- **Release-shaped README template:** the 13-part structure the skill requires,
  from a three-sentence abstract to the licence section, with guidance for each
  part and an optional Screenshots section that this page omits.
- **Plain-language opening:** the abstract and the repository description use
  everyday words, with no technical terms, so a newcomer understands the project
  on the first reading.
- **Attribution template:** an upstream table and a compliance checklist for
  components that are patched, pinned, or only linked.
- **Independent verification:** a fresh directory containing only the release
  tree, a short run, and a deterministic comparison, with untested items named.
- **Approval-gated publishing:** new repositories are initialised in the clean
  tree; existing ones get a branch and preferably a pull request, never a
  force-push.
- **Report contract:** each run ends with destination, contribution,
  third-party handling, audit result, reproduction evidence, and changes.

## Not for / limitations

- **Judgement, not automation.** The skill defines the sequence and the gates;
  the agent using it still classifies files and decides licence questions.
- **No licence determination.** When provenance or obligations are unclear it
  stops and reports, rather than guessing a licence.
- **Requires Git, and `gh` or a remote for publishing.** Without credentials or
  approval it leaves a prepared local tree and stops.
- **Templates are skeletons.** Placeholder rows must be replaced with verified
  metadata; the skill does not populate them.
- **Hardware-dependent claims stay untested** unless the machine is available;
  the release records the gap instead of filling it.
- **No enforcement.** A careless operator can still publish against the skill's
  advice.

## Reproduction environment

| Component | Requirement |
| --- | --- |
| Operating system | Any POSIX system with a shell; recorded on Nobara 44, kernel 7.2.11, x86_64 |
| Language/compiler | Markdown and YAML front matter only; no build step |
| Hardware | None; a workspace and a GitHub destination are the inputs |
| Libraries | Git; optional GitHub CLI for publishing; an Agent Skills-capable harness |
| Input | A project working directory, and for publishing an approved repository and visibility |

## Install and run

```bash
LOCAL_AI=${LOCAL_AI:-$HOME/.config/local-ai}
mkdir -p "$HOME/.agents/skills"
git clone https://github.com/ThomasTZh/dsh-skill-pub-gh "$HOME/.agents/skills/pub-gh"
ln -sfn "$HOME/.agents/skills/pub-gh" "$LOCAL_AI/skills/on-request/pub-gh"
```

`~/.agents/skills` is the shared Agent Skills root scanned by the harness default
and by other compatible agents. The symlink into the on-request directory covers
presets that read only their explicit roots.

Expected output: the harness lists one `skill:pub-gh` entry that resolves to the
cloned `SKILL.md`. Ask the agent to publish or release a project; the skill loads
on that request and follows [`SKILL.md`](SKILL.md), copying the relevant template
into the release tree.

## Layout

| Component | Path | Contents | Class |
| --- | --- | --- | --- |
| Skill method | `SKILL.md` | Rules, house style, seven workflow stages, final report contract | Original |
| Release README skeleton | `assets/README.template.md` | 13-part structure with section guidance and placeholder markers | Original |
| Attribution skeleton | `assets/THIRD_PARTY.template.md` | Upstream project and licence table, compliance checklist | Original |
| Project description | `README.md` | This page | Original |
| Licence | `LICENSE` | MIT, covering the original files | Original |
| Attribution record | `THIRD_PARTY.md` | Host and dependency licences, unresolved items | Original |
| Agent Skills specification | — | Front matter and discovery format the skill follows [1] | Third-party |
| DeepSeek Harness | — | Host that discovers and loads the skill [4] | Third-party |
| Git and GitHub CLI | — | Publish-time tools, not bundled | Third-party |

No upstream file is copied into this repository.

## Results

| Check | Conditions | Result |
| --- | --- | --- |
| Front matter | Parse `SKILL.md`; `name` is kebab-case and matches the installed directory | Pass: `name: pub-gh`, description present |
| README structure | Parse `README.md` and `assets/README.template.md`; compare section sets and order | Pass: template has all 11 sections; README matches with Screenshots omitted |
| Attribution template | Parse `assets/THIRD_PARTY.template.md`; check its sections and the upstream table | Pass |
| Skill discovery | Recorded with `pi --mode rpc --offline` and a `get_commands` request under a temporary `HOME` | Pass at first publication; not re-run for this revision |
| Harness catalogue | Recorded with the skill installed under `~/.agents/skills` and symlinked into the on-request root | Pass at first publication; not re-run for this revision |

Not tested: whether a model loads the skill when the described task appears,
which depends on the model and the request.

## Acknowledgements

- The Agent Skills specification [1] defines the front matter and discovery
  format this skill follows.
- `dsh-setup` [2] and `dsh-mobile` [3] supplied the release practice and the
  report shape that the workflow was distilled from.
- DeepSeek Harness [4] is the host that loads the skill; Git and the GitHub CLI
  perform the publishing step.

## References

1. Agent Skills specification. <https://agentskills.io/specification>
2. `dsh-setup`. <https://github.com/ThomasTZh/dsh-setup>. MIT.
3. `dsh-mobile`. <https://github.com/ThomasTZh/dsh-mobile>. MIT.
4. DeepSeek Harness. <https://github.com/deepseek-ai/deepseek-harness>. MIT.

## Licenses

- **Original files:** `SKILL.md`, `assets/README.template.md`,
  `assets/THIRD_PARTY.template.md`, `README.md`, and `THIRD_PARTY.md` are
  covered by the MIT [`LICENSE`](LICENSE), © 2026 Thomas.
- **Third-party components:** none are redistributed. The specification, host,
  and tools listed above keep their own terms; see [`THIRD_PARTY.md`](THIRD_PARTY.md).
- **Installed separately:** DeepSeek Harness, Git, and the GitHub CLI are not
  bundled with this repository.
