# AUR Packages

This repository contains [my](https://aur.archlinux.org/account/silvan) PKGBUILDs for the [Arch User Repository (AUR)](https://aur.archlinux.org/).

All packages are kept in a single repository, organized into individual subdirectories for each package.

## Management

This repository is maintained and published using [aurpublish](https://github.com/eli-schwartz/aurpublish).

* Each package is updated within its own directory.
* `aurpublish` git hooks automatically handle `.SRCINFO` generation and basic syntax checking on commit.
* Packages are synced to the AUR using the `aurpublish <package>` command, which pushes the subdirectory history to the respective AUR remote.

## Contributing

Issues and pull requests are welcome! If you notice an out-of-date package, find a bug, or have an improvement, feel free to open an issue or submit a PR.

