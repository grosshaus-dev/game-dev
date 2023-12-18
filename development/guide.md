# Our Game Development Guide

## Development Cycle

The cycle for the initial version of the game and any features added in the future. Bug fixes won't follow this cycle.

Brainstorm -> Prototype -> Refactor -> Populate -> Polish -> Publish

### Brainstorm

### Prototype

Example build: [0.1.0-alpha.7] *Prototype*

Do
- Use Blueprints.
- Keep you project organized.
- Use placeholder art.
- Use placeholder sound.
- Let other people play it!
- Fix bugs that impact gameplay negatively.

Don't
- Use C++ unless absolutely necessary.
- Care about performance.
- Try to fix minor bugs.

Once it's fun to play, move to the next phase. If it's not fun, go back to brainstorming.

### Refactor

Example build: [0.1.0-alpha.8] *Refactor*

Do
- Move candidate logic to C++, [this article](https://docs.unrealengine.com/4.27/en-US/Resources/SampleGames/ARPG/BalancingBlueprintAndCPP/) explains where to start.
- Do general performance optimizations.
- Fix minor bugs in the core mechanics.

Don't
- Start polishing things.

### Populate

Example build: [0.1.0-beta.1] *Populate*

The final build in this phase will be the first beta build.

Do
- Add all the content planned for current release. Levels, items, characters.

### Polish

Example build: [0.1.0-rc.1] *Polish*

The final build in this phase will be the first release candidate.

Do
- Replace art with production ready versions.
- Replace sound with production ready sound.
- Optimize levels for performance.
- Measure performance on end-devices and optimize where necessary.

Don't
- Add any new features. Just log your ideas and add them in the next iteration.

### Publish

Example build: [0.1.0] *Publish*

Do
- Build release versions and test them.
- Fix critical bugs that come up in release versions.

## Versioning

Use Git, [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and adhere to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

### Git

#### Branches

- Work on the next release is done on the `next` branch.
- Non-trivial features or bugfixes for the next release get their own branches.
- Trivial features or bugfixes, those that can be finished in a day, don't get their own branch. They are implemented locally and then committed to the `next` branch in a single commit. If you notice that what you are implementing is not trivial, create a branch for it.
- Bugfixes for the current release always get their own branch.

Branch Type               | Prefix  | Name              | Parent Branch
---                       |---      |---                |---
Feature for next release  | f-      | feature name      | next
Patch for next release    | p-      | issue number      | next
Patch for current release |         | patch number      | release

```
|-- main
    |-- release
        |-- 0.1.24
    |-- next
        |-- f-saving
        |-- f-genetics
        |-- p-34
        |-- p-39
```

#### Commits

- Never re-write history that is not local or on a feature branch.
- Squash commits that you have made locally while working on a trivial new feature.
- Squash commits that you have made in a feature branch when merging it to the `next` branch.

**As always, go have a coffee, think about it, then push.**

#### Issues

Use issues for bugs only. The goal is always to have no open issues for the current stable release.

### Changelog

Keep track of all changes in a changelog based on the [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) format.

### Semantic Versioning

Adhere to [Semantic Versioning](https://semver.org/spec/v2.0.0.html). The *public API* of the game in the context of Semantic Versioning is the save games created on a players computer. Whether a release is minor or major depends solely on save game compatibility, not on how much is implemented.

Pre-release versions are treated as follows:

- Alpha builds: -alpha.*alpha-build-number* is appended.
- Beta builds: -beta.*beta-build-number* is appended.
- Release candidate builds: -rc.*release-candidate-build-number* is appended.

Example of builds leading up to a minor release and patches after it.

- 0.1.0-alpha.1
- ...
- 0.1.0-alpha.21
- 0.1.0-beta.1
- ...
- 0.1.0-beta.17
- 0.1.0-rc.1
- ...
- 0.1.0-rc.5
- 0.1.0
- ...
- 0.1.24


## Style guides

### Unreal Engine 5

For the contents of the UE5 project the following guides are followed. Guides take precedence over each other the higher up on the list they are.

- [Unreal Naming Convention Guide](https://www.tomlooman.com/unreal-engine-naming-convention-guide/).
- [Gamemakin LLC Style Guide](https://github.com/Allar/ue5-style-guide).

### C++

For C++ all parts of the [Epic C++ Coding Standard for Unreal Engine](https://docs.unrealengine.com/5.1/en-US/epic-cplusplus-coding-standard-for-unreal-engine/) is followed.

In addition the following rules are to be adhered to.

1. All C++ functions that get exposed to Blueprints (`public` or `protected` with `UFUNCTION(BlueprintCallable)` set) must:
   - have the name of the project appended to them, e.g., `OurProjectAwesomeFunction`.
   - have a category set that starts with the name of the project, e.g., `UFUNCTION(BlueprintCallable, Category="OurProject AI")`.
