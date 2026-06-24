# flatpak.mser.at

[![Lint status][badge-lint-status]][badge-lint-status-url]
[![Build status][badge-build-status]][badge-build-status-url]

> Various things missing from Flathub

This deploys a [Flatpak][flatpak] repository that contains various things that
are currently not available on [Flathub][flathub]. The main use case right now
is for installing a couple of roguelike games on the [Steam Deck][steam-deck]
(as Flatpak is what it supports out-of-the-box and what will survive system
updates without manual intervention), hence why there aren't any other packages
available (for now).

Both `x86_64` and `aarch64` variants are available and all packages are rebuilt
automatically once a week.

## Available applications

| Name                                     | ID                                                           | Type | Notes                                                                                                  |
| ---------------------------------------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------------------------------------------------ |
| [Infra Arcana][app-infra-arcana-website] | [`com.gitlab.martintornqvist.InfraArcana`][app-infra-arcana] | Game |                                                                                                        |
| [Sil-Q][app-sil-q-website]               | [`com.github.silquirk.SilQ`][app-sil-q]                      | Game | See [here][app-sil-q-using-x11] if you encounter an error when trying to launch using the X11 frontend |

## Usage

### Adding the repository

To add the repository, use the `flatpak remote-add` command:

```sh
flatpak remote-add --if-not-exists flatpak.mser.at https://flatpak.mser.at/index.flatpakrepo
```

Alternatively, if you have a GUI client for Flatpak (e.g.,
[Discover][discover], if you are using a Steam Deck) you should be able to
download the [flatpakrepo file][flatpakrepo-file] and just double-click it.

[discover]: https://apps.kde.org/de/discover/
[flatpakrepo-file]: https://flatpak.mser.at/index.flatpakrepo

### Listing available applications

To list all available applications, use the `flatpak remote-ls` command:

```sh
flatpak remote-ls flatpak.mser.at
```

### Installing applications from the repository

To install an application, use the `flatpak install` command:

```sh
flatpak install flatpak.mser.at com.gitlab.martintornqvist.InfraArcana
```

## Breaking changes

Sometimes a change requires manual intervention on existing installations.
These are listed here, newest first (and removed once they are no longer
relevant):

- __[2026-06-24] - The repository is signed with a new GPG key:__ if you added
  the repository before this date, `flatpak` refuses to update the installed
  applications because the new signature no longer matches the pinned key.
  Remove and re-add the repository to pin the new key (installed applications
  and their data are kept):

  ```sh
  flatpak remote-delete --force flatpak.mser.at
  flatpak remote-add --if-not-exists flatpak.mser.at https://flatpak.mser.at/index.flatpakrepo
  ```

## Maintainer

[Michael Serajnik][maintainer]

## Contribute

You are welcome to help out!

[Open an issue][issues] or [make a pull request][pull-requests].

## Licenses

- [`AGPL-3.0-or-later`][license-agpl-3.0-or-later] (Code and the Infra Arcana
  icon)
- [`CC-BY-SA-4.0`][license-cc-by-sa-4.0] (Documentation)
- [`CC0-1.0`][license-cc0-1.0] (Configuration and packaging metadata)
- [`LicenseRef-Sil-Q-icon`][license-sil-q-icon] (Sil-Q icon)

This project follows the [REUSE specification][reuse-spec].

[app-infra-arcana]: https://github.com/mserajnik/flatpak.mser.at/tree/master/apps/com.gitlab.martintornqvist.InfraArcana
[app-infra-arcana-website]: https://sites.google.com/site/infraarcana/
[app-sil-q]: https://github.com/mserajnik/flatpak.mser.at/tree/master/apps/com.github.silquirk.SilQ
[app-sil-q-using-x11]: https://github.com/mserajnik/flatpak.mser.at/tree/master/apps/com.github.silquirk.SilQ#using-the-x11-frontend
[app-sil-q-website]: https://github.com/sil-quirk/sil-q
[badge-build-status]: https://github.com/mserajnik/flatpak.mser.at/actions/workflows/build-and-deploy.yaml/badge.svg
[badge-build-status-url]: https://github.com/mserajnik/flatpak.mser.at/actions/workflows/build-and-deploy.yaml
[badge-lint-status]: https://github.com/mserajnik/flatpak.mser.at/actions/workflows/lint.yaml/badge.svg
[badge-lint-status-url]: https://github.com/mserajnik/flatpak.mser.at/actions/workflows/lint.yaml
[flathub]: https://flathub.org/
[flatpak]: https://flatpak.org/
[issues]: https://github.com/mserajnik/flatpak.mser.at/issues
[license-agpl-3.0-or-later]: LICENSES/AGPL-3.0-or-later.txt
[license-cc-by-sa-4.0]: LICENSES/CC-BY-SA-4.0.txt
[license-cc0-1.0]: LICENSES/CC0-1.0.txt
[license-sil-q-icon]: LICENSES/LicenseRef-Sil-Q-icon.txt
[maintainer]: https://github.com/mserajnik
[pull-requests]: https://github.com/mserajnik/flatpak.mser.at/pulls
[reuse-spec]: https://reuse.software/spec/
[steam-deck]: https://www.steamdeck.com/
