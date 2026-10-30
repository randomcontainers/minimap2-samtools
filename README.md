# minimap2-samtools

Minimap2 with Samtools, for aligning long reads and sorting and indexing the alignments as BAM.

This image is the default image of [minimap2](https://github.com/randomcontainers/minimap2) (`ghcr.io/randomcontainers/minimap2:latest`), published under its own name. The contents are the same; the digests differ. It contains Minimap2 and Samtools, on Ubuntu or Alpine, for `linux/amd64` and `linux/arm64`.

These are unofficial builds, not affiliated with or endorsed by the upstream projects. Report problems with the image in [randomcontainers/minimap2](https://github.com/randomcontainers/minimap2/issues) and problems with a tool itself in that tool's own issue tracker.

## Quick start

```sh
docker run --rm --user "$(id -u):$(id -g)" -v "$PWD:/work" ghcr.io/randomcontainers/minimap2-samtools -ax map-ont -t 8 -o aln.sam ref.fa reads.fq.gz
```

The examples in the [minimap2 README](https://github.com/randomcontainers/minimap2#readme) work with this image too.

## Tags

`<version>` is the Minimap2 version.

| Tags | Base |
|---|---|
| `latest`, `<version>`, `ubuntu`, `<version>-ubuntu`, `<version>-ubuntu26.04` | Ubuntu 26.04 |
| `alpine`, `<version>-alpine`, `<version>-alpine3.24` | Alpine 3.24 |

`latest` and `<version>` are the Ubuntu 26.04 images. The images are currently built on Ubuntu 26.04 and Alpine 3.24. Tags without a distro version move to the next distro release when the project does; tags ending in `ubuntu26.04` or `alpine3.24` stay on that release and are no longer rebuilt once the project moves to the next one.

Only the tags of the Minimap2 version currently in [minimap2's package.yml](https://github.com/randomcontainers/minimap2/blob/main/package.yml) are rebuilt, exact-version tags included, so pin a digest when you need the same bytes every time. Tags of older versions stay as they were last built. The published tags and their digests are listed on the [package page](https://github.com/orgs/randomcontainers/packages/container/package/minimap2-samtools).

## Platforms

`linux/amd64` and `linux/arm64`, both built natively on GitHub-hosted runners.

## Files and permissions

The working directory is `/work`. The image runs as UID 1000, and any other UID works too: `HOME` is then `/`, and caches go to `/cache`, which anyone can write to. How to get output files owned by you depends on how you run containers:

| Runtime | Flag |
|---|---|
| Docker on Linux (rootful), GitHub Actions | `--user "$(id -u):$(id -g)"` |
| Rootless Podman | `--userns=keep-id` |
| Rootless Docker | `--user 0:0` (root in the container is your user on the host) |
| Docker Desktop on macOS or Windows | none, file ownership is mapped for you |

## Contents

| Package | License | Repository |
|---|---|---|
| [Minimap2](https://github.com/lh3/minimap2) | `MIT AND BSD-3-Clause` | [randomcontainers/minimap2](https://github.com/randomcontainers/minimap2) |
| [Samtools](https://www.htslib.org/) | `MIT AND BSD-3-Clause AND BSD-2-Clause AND CC0-1.0 AND LicenseRef-Public-Domain` | [randomcontainers/samtools](https://github.com/randomcontainers/samtools) |

## Verifying

Each image has a build provenance attestation from this repository's GitHub Actions run. The run uses the shared build workflow of [randomcontainers/ci](https://github.com/randomcontainers/ci), which signs the attestation, so name both repositories:

```sh
gh attestation verify oci://ghcr.io/randomcontainers/minimap2-samtools:latest \
  --repo randomcontainers/minimap2-samtools --signer-repo randomcontainers/ci
```

Images from `ghcr.io/randomcontainers/minimap2` are built in [randomcontainers/minimap2](https://github.com/randomcontainers/minimap2), so verify them with `--repo randomcontainers/minimap2 --signer-repo randomcontainers/ci`.

## Updates

The images are rebuilt when a new image of a package above is published, for example after an upstream release. They are also rebuilt when the base image changes and at least every 7 days, so distro security fixes reach the current tags. The package repositories describe how each upstream release is picked up.

## Licenses

The image contents are licensed under `MIT AND BSD-3-Clause AND BSD-2-Clause AND CC0-1.0 AND LicenseRef-Public-Domain`. The version of each package is in `/usr/local/share/randomcontainers/<package>/version` and its license files are in `/usr/local/share/randomcontainers/<package>/licenses/`.

Ubuntu and Alpine packages keep their own licenses. The SBOM of each platform image lists them with their versions:

```sh
docker buildx imagetools inspect ghcr.io/randomcontainers/minimap2-samtools:latest --format '{{ json .SBOM }}'
```

The files in this repository are available under the MIT license, see [LICENSE](LICENSE).

## Requesting a tool

To suggest another tool, use the [Request a tool](https://github.com/randomcontainers/.github/issues/new?template=tool-request.yml) form.

## This repository

The files here are generated from the `combos` section of `package.yml` in [randomcontainers/minimap2](https://github.com/randomcontainers/minimap2). Open issues and pull requests there.
