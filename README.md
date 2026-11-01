# dsh-skill-pub-gh

A skill for publishing a project to GitHub as a minimal, reproducible release instead of a mirror of a working directory.

## Abstract

A working directory is a poor release: it carries credentials, local paths, logs, caches, and third-party code whose licence may not allow redistribution. This skill turns "publish this" into a checked sequence: classify every file as original, modified upstream, or upstream, build a clean allowlist tree, run privacy and licence gates, write a release-shaped README with a verification table, verify from a fresh directory, and only then push after explicit approval. It is an instruction file plus two documentation templates.

## Contents

| Path | Contents |
|---|---|
| [`SKILL.md`](SKILL.md) | The method: rules, house style, seven workflow stages, and the final report contract |
| [`assets/README.template.md`](assets/README.template.md) | Release-shaped README skeleton: abstract, methods, results, conclusion, acknowledgements, references |
| [`assets/THIRD_PARTY.template.md`](assets/THIRD_PARTY.template.md) | Attribution and licence-compliance skeleton for upstream components |

## Install

```sh
LOCAL_AI=${LOCAL_AI:-$HOME/.config/local-ai}
mkdir -p "$HOME/.agents/skills"
git clone https://github.com/ThomasTZh/dsh-skill-pub-gh "$HOME/.agents/skills/pub-gh"
ln -sfn "$HOME/.agents/skills/pub-gh" "$LOCAL_AI/skills/on-request/pub-gh"
```

`~/.agents/skills` is the shared Agent Skills root scanned by the harness default and by other compatible agents. The symlink into the on-request directory covers presets that read only their explicit roots.

## Verification

| Check | Command | Result |
|---|---|---|
| Front matter | parse `name` and `description`, check the name is kebab-case and the directory name matches | pass: `name: pub-gh`, description present |
| Discovery | temporary `HOME`, then `pi --mode rpc --offline` with a `get_commands` request | pass: one `skill:pub-gh` entry resolving to the cloned `SKILL.md` |
| Templates parse | read both `assets/*.md` files and check their headings and placeholder markers | pass |
| Harness catalogue | installed under `~/.agents/skills` and symlinked into the on-request root | pass: the running harness listed it without a restart |

**Not tested:** whether a model loads the skill when the described task appears, which depends on the model and the request.

## Limitations

- The skill enforces judgement, not automation: the classification and the licence decisions are made by the agent using it.
- It assumes `git` and an authenticated `gh` or remote for the push step, and stops before publishing when approval or credentials are missing.
- The templates are skeletons. Placeholder rows must be replaced with verified metadata before publication.

## Acknowledgements

The skill format follows the Agent Skills specification [1]; the method is original and was shaped by actual releases [2] [3].

## References

1. Agent Skills specification. <https://agentskills.io/specification>.
2. `dsh-setup`. <https://github.com/ThomasTZh/dsh-setup>. MIT.
3. `dsh-mobile`. <https://github.com/ThomasTZh/dsh-mobile>. MIT.
