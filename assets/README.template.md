# <Project title>

<Three sentences at most: what this repository contains, what it does, and the strongest verified fact about it. No citations, no implementation detail.>

## Purpose and gaps

<One sentence: what the project is for.>

- **Gap:** <the capability, evidence, or tooling that existing work does not provide, cited [1].>
- **Approach:** <how this repository closes it, in one sentence.>

## Features

- <Capability a user can exercise — name the command, entry point, or file that provides it.>
- <Keep one bullet per capability; drop roadmap items and duplicates.>

## Not for / limitations

- <What the project deliberately does not do.>
- <Hardware, data, calibration, or licensing constraint that limits replication.>
- <Anything not tested, stated plainly.>

## Screenshots

![<what the image demonstrates>](<relative path>)

<Second image only if it adds information. Delete this section entirely when no verified screenshot exists; never ship a placeholder.>

## Reproduction environment

| Component | Requirement |
| --- | --- |
| Operating system | <version/architecture> |
| Language/compiler | <version> |
| Hardware | <model/interface; driver/firmware where applicable> |
| Libraries | <direct dependencies with pinned versions> |
| Input | <small synthetic or permission-cleared input, its format and provenance> |

## Install and run

```bash
# 1. Obtain
<clone or release download command>

# 2. Install
<exact verified install command>

# 3. Configure
<copy example config to a local name; placeholders only, no credentials>

# 4. Run
<exact verified run or test command>
```

Expected output: <filename, shape, units, tolerance, or observable behaviour>.

## Layout

| Component | Path | Contents | Class |
| --- | --- | --- | --- |
| <name> | `<path>` | <what it contains> | Original |
| <name> | `<path>` | <what changed relative to [2]> | Modified third-party |
| <dependency name> | — | <upstream version and purpose; not copied> | Third-party |

Third-party attribution, licences, and patch reconstruction are in [THIRD_PARTY.md](THIRD_PARTY.md).

## Results

| Test / metric | Conditions | Result |
| --- | --- | --- |
| <verified test> | <hardware/software/input> | <measured value and unit, or pass/fail> |

<One or two sentences interpreting only what the evidence establishes. Cite external datasets or methods [3]. If nothing was measured, say so rather than implying a result.>

## Acknowledgements

- <Upstream author/project [1]: what was used or changed; preserve original copyright.>
- See [THIRD_PARTY.md](THIRD_PARTY.md) for complete attribution and modification records.

## References

1. <Authors, title, venue/year or software/version, DOI or official URL, repository, licence link.>
2. <Repeat for every reused method, dataset, figure, and component.>

## Licenses

- **Original files:** <licence name> — see [LICENSE](LICENSE), which lists the files it covers.
- **Third-party components:** <licence names and where their notices live> — see [THIRD_PARTY.md](THIRD_PARTY.md).
- **Obtained separately by the user:** <proprietary software, hardware, or restricted data, if any; otherwise delete this bullet.>
