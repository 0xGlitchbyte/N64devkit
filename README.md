# N64 Development Kit

## Summary

*Develop C games for the Nintendo 64. Includes Debian C/C++ build tools as well as the N64 modern-sdk toolchain by CrashOveride.*

| Metadata | Value |  
|----------|-------|
| *Categories* | Core, Languages |
| *Image type* | Dockerfile |
| *Published images* | mcr.microsoft.com/devcontainers/focal |
| *Available image variants* | debian-11, debian-10, ubuntu-22.04, ubuntu-20.04, ubuntu-18.04 ([full list](https://mcr.microsoft.com/v2/devcontainers/cpp/tags/list)) |
| *Published image architecture(s)* | x86-64, aarch64/arm64 for `debian-11`, `ubuntu-22.04`, and `ubuntu-18.04` variants |
| *Container host OS support* | Linux, macOS, Windows |
| *Container OS* | Debian, Ubuntu |
| *Languages, platforms* | C |

## Setting up your enviornment for the N64 Development Kit

1. Download and install [VSCode](https://code.visualstudio.com/Download).
2. Download and install [Docker](https://docs.docker.com/get-docker/)
3. Open VSCode and look for "Extensions" tab. Open it.
4. Search for "Remote Containers". Install it.
5. `ctrl+shift+p` or `cmd+shift+p` to open up a VSCode command prompt. Type in `Remote-Containers: Clone Repository in Container Volume`. Allow it to reach out to Github.
6. Type in `MrGlitchByte/N64devkit` for repo.
7. Choose the branch you want to pull. **NOTE**: It takes a while to clone. Get a cup of coffee or take a 5 minute break.

## Using this image

You can directly reference pre-built versions of `Dockerfile` by using the `image` property in `.devcontainer/devcontainer.json` or updating the `FROM` statement in your own  `Dockerfile` to one of the following. An example `Dockerfile` is included in this repository.

- `mcr.microsoft.com/devcontainers/debian` (latest Debian GA)
- `mcr.microsoft.com/devcontainers/debian-11` (or `bullseye`)
- `mcr.microsoft.com/devcontainers/debian-10` (or `buster`)
- `mcr.microsoft.com/devcontainers/ubuntu` (latest Ubuntu LTS)
- `mcr.microsoft.com/devcontainers/ubuntu-22.04` (or `jammy`)
- `mcr.microsoft.com/devcontainers/ubuntu-20.04` (or `focal`)
- `mcr.microsoft.com/devcontainers/ubuntu-18.04` (or `bionic`)

You can decide how often you want updates by referencing a [semantic version](https//semver.org/) of each image. For example

- `mcr.microsoft.com/devcontainers/0-bullseye`
- `mcr.microsoft.com/devcontainers/0.205-bullseye`
- `mcr.microsoft.com/devcontainers/0.205.0-bullseye`

However, we only do security patching on the latest [non-breaking, in support](https://github.com/devcontainers/images/issues/90) versions of images (e.g. `0-debian-11`). You may want to run `apt-get update && apt-get upgrade` in your Dockerfile if you lock to a more specific version to at least pick up OS security updates.

You can use the contents of `Dockerfile` to fully customize your container's contents or to build it for a container host architecture not supported by the image.

Beyond `git`, this image / `Dockerfile` includes `zsh`, [Oh My Zsh!](https://ohmyz.sh/), a non-root `vscode` user with `sudo` access, a set of common dependencies for development, and [Vcpkg](https://github.com/microsoft/vcpkg) a cross-platform package manager for C/C++.

It also includes the Visual Studio Code extensions `C/C++ Tools`, `C/C++ Extension Pack`, and `C/C++ Advanced Linting`.

### Using Vcpkg
This dev container and its associated image includes a clone of the [`Vcpkg`](https://github.com/microsoft/vcpkg) repo for library packages, and a bootstrapped instance of the [Vcpkg-tool](https://github.com/microsoft/vcpkg-tool) itself.

The minimum version of `cmake` required to install packages is higher than the version available in the main package repositories for Debian (<=11) and Ubuntu (<=21.10).  `Vcpkg` will download a compatible version of `cmake` for its own use if that is the case (on x86_64 architectures).

Most additional library packages installed using Vcpkg will be downloaded from their [official distribution locations](https://github.com/microsoft/vcpkg#security). To configure Vcpkg in this container to access an alternate registry, more information can be found here: [Registries: Bring your own libraries to vcpkg](https://devblogs.microsoft.com/blog/registries-bring-your-own-libraries-to-vcpkg/).

To update the available library packages, pull the latest from the git repository using the following command in the terminal:

```sh
cd "${VCPKG_ROOT}"
git pull --ff-only
```

> Note: Please review the [Vcpkg license details](https://github.com/microsoft/vcpkg#license) to better understand its own license and additional license information pertaining to library packages and supported ports.
