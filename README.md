# Jellyfin Debian Packaging

This repository contains the Debian packaging configuration for Jellyfin. This repository can be used to generate Debian/Ubuntu `.deb` packages, source packages, and supplemental files for Jellyfin on a number of architectures.

This repository replaces the previous `deployment/debian-package-*` and `deployment/ubuntu-package-*` sections of the [main Jellyfin repository](https://github.com/jellyfin/jellyfin), in order to fully separate the Debian packaging from the main code repository.

## Build Dependencies

For the easiest build experience, the following packages are required to build Jellyfin `.deb` packages:

#### Debian packaging dependencies

* `dpkg-dev` [contains `dpkg-buildpackage`]
* `devscripts` [contains `uscan`]

#### Jellyfin build dependencies

* `dotnet-sdk-X.X`, either 2.2 (for 10.4.z and older) or 3.0 (for 10.5.z and newer)
* `npm` or `nodejs` providing an `npm` binary
* `libssl1.X-dev`, where `X` is either `0` or `1` depending on the distro (most support `1`)

## Performing a Build

The build contains two main steps - preparing the repo, and building:

#### Preparation

1. Clone down the `jellyfin-debian` repository.

1. Enter the directory, and ensure the `debian/changelog` reflects the version you want to build; `master` is a valid value here.

1. Enter the `jellyfin-debian` repository directory.

1. Run `uscan -vddd` to force a download of the source archive. This will be automatically unpacked at `../jellyfin-<version>`.

#### Build

1. Enter the now-prepared Debian source directory at `../jellyfin-<version>`.

1. Run `sudo dpkg-buildpackage -us -uc -jX`, where `X` is a thread count (usually your number of CPU cores).

1. Enjoy your `jellyfin*.deb` packages at `../`.
