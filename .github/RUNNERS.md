# GitHub Actions runners

Linux jobs use the repository variable `UBICLOUD_RUNNER`. With no value set,
they use `ubuntu-latest`. macOS and Windows jobs keep their existing runner labels.

## Activate Ubicloud

1. Install **Ubicloud Managed Runners** on Studio65-AI with access to this repository
   and connect it to Ubicloud project `pj9hwy6g905p1gc4nsamjbmb4k`.
2. Set the **repository-level** Actions variable `UBICLOUD_RUNNER` to
   `ubicloud-standard-4-ubuntu-2404` (Linux x64, 4 vCPU, 16 GB RAM).
3. Run the repository checks and confirm the job's runner name and labels in
   GitHub Actions and the matching job in the Ubicloud console.

Use a repository variable, not an environment variable: runner selection happens
before environment-level variables become available. Premium routing is enabled
by default in Ubicloud; check GitHub Runners → Settings for the selected fleet and
its billing rate before activation.

## Roll back

Delete the repository variable `UBICLOUD_RUNNER`, or set it to `ubuntu-latest`,
then cancel and rerun affected queued/failed workflows. Existing jobs do not move
runners when the variable changes. The fallback applies when the variable is
empty; it does not detect Ubicloud outages or an invalid label.

Runner migration does not change workflow triggers, secrets, deployment targets,
or release approvals. Release/deployment workflows still have their existing
side effects; use normal checks to verify the runner before dispatching a release.

References: [setup](https://www.ubicloud.com/docs/github-actions-integration/quickstart),
[runner labels](https://www.ubicloud.com/docs/github-actions-integration/runner-types),
[pricing](https://www.ubicloud.com/docs/about/pricing).
