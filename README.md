# AArch64 Prebuilt GCCs

Bleeding edge GNU/Linaro GCC toolchains built from sources using latest git version of [crosstool-NG](https://github.com/crosstool-ng/crosstool-ng). These prebuilt toolchains are primarily for building kernels, hence only CC compiler is exist. Additionally, all toolchains are generic-optimized so it should be compatible with all ARM64 devices.

## Notice

If you've no idea on how to improve this README file, it's better to not even fork this repository; just clone and use it. Forking a repository for nothing other than bumping your repository count is a waste of resources.

_People are becoming more and more weird these days._

## Cloning the toolchain

Run this command anywhere on your environment:

```bash
$ git clone git://github.com/krasCGQ/aarch64-linux-android -b <branch> --depth=1
```

Where `<branch>` is one of these branches:
* `a53-7.x` - GNU GCC 7.2.1, optimized for Cortex-A53 (deprecated)
* `opt-gnu-7.x` - GNU GCC 7.3.1 (deprecated)
* `opt-gnu-8.x` - GNU GCC 8.2.1
* `opt-linaro-7.x` - Linaro GCC 7.3.1

## Using the toolchain

I'm assuming that you're building kernels and have all patches included in your kernel source. For that, pass `CROSS_COMPILE` variable as one of `make` parameters.

```bash
$ make ARCH=arm64 CROSS_COMPILE=</path/to/toolchain>/bin/aarch64-opt-linux-android- ...
```

I recommend this way since exporting `CROSS_COMPILE` doesn't always work.

Have something wrong? It's your own job to figure and fix all issues you may counter.

Also, to be warned: This toolchain is NOT COMPATIBLE for use with clang.

## Resources

* [crosstool-NG defconfig](https://github.com/krasCGQ/ct-ng_configs/blob/master/config.aarch64-android)
* [Script to update git projects and merge crosstool-NG patches](https://github.com/krasCGQ/scripts/blob/master/update_crosstool)
* [ISL patch](https://github.com/krasCGQ/patches/blob/master/isl/0001-isl--Revert-all-troublesome-changes.patch) (essentialy reverts) - _required if you choose to use latest ISL from git as one of your self-built toolchain components_
