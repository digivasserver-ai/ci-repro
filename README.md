# ci-repro — microG GmsCore build mirror

Purpose: run microG's CI on code that cannot run it directly (fork PR workflows
sit behind the first-time-contributor approval gate on `microg/GmsCore`).

- Tree: `master` = snapshot of `digivasserver-ai/GmsCore` branch
  `droidguard/pi-multistep-v2` (PR microg/GmsCore#3750) — droidguard files
  byte-identical to the PR head.
- CI: `.github/workflows/build.yml` is byte-identical to microG's
  `.github/workflows/build.yml` (Debug + Release matrix, `assemble` + `lint`,
  Temurin JDK 17, gradle/actions v6).

## Runs

| run | commit | result |
| --- | --- | --- |
| 33248113409 | 0423616 (pre-fix) | fail — `:play-services-droidguard-core:compileReleaseKotlin` (K/V inference) |
| 33248919469 | 654b320 (fix: `mutableMapOf<Any?, Any?>()`) | pass — Debug + Release |

Provenance: 0423616 = snapshot of PR branch before fix cd512b9; 654b320 = that
tree + the exact one-line fix from cd512b9.
