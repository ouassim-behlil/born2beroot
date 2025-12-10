# What is dpkg, apt, and aptitude?

## dpkg:

- `dpkg` is the base package management tool on Debian and Debian based systems. It handles the low level task of installing, removing, configuring and querying `.deb` packages.

- it does not fetch packages from online repos; it only works with `.deb` files you have locally(manually downloaded).

- `dpkg` also does not automatically resolve dependencies: so if a package depends on other one, you should ensure the dependencie is present.

- in short: `dpkg` is low-level, minimal package tool.

## APT/apt/apt-get

- APT (the Advanced Package Tool) is a higher-level package management infrastructure that builds on top of `dpkg`. it adds repository management, dependencies resolution, downloading packages, version management...

- Tools like `apt-get`, `apt-cache` and `apt` are front-ends to APT. `apt` is more modern, user firendly CLI front-end that unifies common tasks.
- `apt install package_name`: APT fetches package (and required dependencies) from configured repositories, download them, then internally calls `dpkg` to install them.

- `apt remove` `apt upgrade`, `apt update`, etc: APT manages metadata, dependencies,  and repository interaction.

- Dependencies are resolved and instelled automatically.

- APT maintains a cache/repository metadata, unlike `dpke` which only sees local `.deb` files.

## aptitude:

- `aptitude` itself is another front-end build on APT (also uses `dpkg` under the hood).

- if offers extra features compared to plain `apt`/`apt-get` text-based interactive interface, more powerful searching/filtering of packages, easier browsing of installed/available packages, and advanced dependency resolution and package state tracking.

- on the command line, `aptitude` commands mirror many of the same tasks as `apt`/`apt-get`.
