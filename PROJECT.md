# Tapas development workspace

## Starting point

- Upstream: https://github.com/Sype0/pmos-tapas
- Downloaded: 2026-11-20
- Original commit: `c5b6ab106f8277908a56b77a6a595d4ad0531dba`
- Local baseline tag: `baseline-2026-11-20`
- GitHub baseline branch: `baseline/2026-11-20`
- Working branch: `work/tapas`
- Device target: Xiaomi Redmi Note 12 4G, codename `tapas` (SM6225).

The upstream README describes this as experimental mainline Linux bring-up,
with builds on GitHub Actions and no successful device boot confirmed there.
The documented memory layout targets the 6 GB model. Confirm the actual phone's
RAM and variant before making device-specific changes.

## Version history

Keep `main` at the downloaded upstream version initially. Make small, named
commits on working branches. Each commit records a recoverable checkpoint;
branches keep separate experiments apart. The baseline tag identifies the
original code even after development moves forward.

To examine the original code without changing the working branch:

```sh
git switch -c inspect/baseline baseline-2026-11-20
```

Return to development with `git switch work/tapas`. Commit or stash pending
edits before switching branches. To undo a committed change while preserving
history, use `git revert COMMIT_SHA` from a clean working tree.

## GitHub publication

`upstream` points to Sype0's original repository. `origin` points to our fork:
https://github.com/justvinc103-svg/pmos-tapas

`main` retains the original upstream version. `baseline/2026-11-20` is the
published original checkpoint, and `work/tapas` holds our setup and experiments.
GitHub writes use the connected GitHub integration. Subsequent changes should
be saved as commits on working branches and reviewed before merging.

This is a personal hobby and learning project by a non-developer. All credit
for the original port goes to Sype0 and upstream contributors; retain existing
license, copyright, and dependency attribution. Our notes and modifications
must be clearly distinguished from the original work.

## Builds and verification

The existing `.github/workflows/build.yml` uses an ARM64 Ubuntu runner and
supports manual builds. Its automatic push trigger currently targets `main`.
It publishes a rolling `latest` prerelease, replacing the previous one; Git
history preserves source checkpoints, but this release is not an image archive.

The current shell machine is x86_64. The existing build script requires a static
AArch64 BusyBox and executes it while checking applets, so a local build needs
an appropriate cross-build/emulation setup or the existing ARM64 CI runner.
No full kernel build or phone test has been performed in this workspace.

## Next development step

Choose the first concrete change with the user, implement it on a feature
branch, run appropriate checks, and record the result in a commit. Preserve the
upstream license. Building a boot image does not establish device compatibility.
