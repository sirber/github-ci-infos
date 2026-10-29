# GitHub CI runner information

Inspect the hardware and disk usage of GitHub-hosted Ubuntu runners. A runner is the machine that executes a workflow job.

One manual workflow starts three independent jobs for `ubuntu-22.04`, `ubuntu-24.04`, and `ubuntu-26.04`. Each job records the image version so that you can compare results across image updates.

## Run the workflow

1. Open [Ubuntu runner specs](https://github.com/sirber/github-ci-infos/actions/workflows/runner-info.yml).
2. Select **Run workflow**.
3. Select the `main` branch.
4. Select **Run workflow** to start all three jobs.
5. Open the completed run to read the job summaries.

For the full output, open a job and expand **Report hardware and disk usage**. The workflow runs only when you start it manually.

## Report contents

Each job reports the following information:

- Ubuntu version, runner image version, and kernel version.
- CPU model, processor details, and available processor count.
- RAM and swap totals, usage, and available space.
- Disk devices, mounted filesystems, disk space, and inode usage. Inodes are filesystem records for files and directories.
- The 50 largest directories within four levels of the root filesystem.
- Sizes of common tool directories, including Android, .NET, Haskell, Swift, and the cache of preinstalled tools.
- The 30 largest files over 500 MiB under `/usr`, `/opt`, `/var`, and `/home`.
- Docker disk usage for images, containers, volumes, and the build cache.

## Interpret the results

The workflow inspects the machine before any project build or cleanup. It does not install dependencies, build images, or delete tools.

Directory sizes include their children. Do not add those totals together. The main directory scan stays on the root filesystem, so it excludes separate filesystems.

Disk usage changes as GitHub updates runner images. Compare the recorded image versions as well as the Ubuntu versions. Results from this repository describe its runners and do not guarantee identical resources for another repository.

The workflow definition is in [runner-info.yml](.github/workflows/runner-info.yml). Each job has a 15-minute limit, and a failed job does not cancel the other Ubuntu jobs.
