# ungoogled-chromium-mobile

This repository contains build scripts and patches for building [Ungoogled Chromium](https://github.com/ungoogled-software/ungoogled-chromium) for Android (arm64) as a mobile browser.

## Goal

Create a privacy-focused Chromium build for Android without Google dependencies, optimized for mobile use.

## Status

Work in progress. Currently preparing build environment on Android/Termux (aarch64) with root access.

## Approach

1. Set up build environment in Termux/Ubuntu container (chroot/proot)
2. Clone ungoogled-chromium repository and apply patches
3. Use depot_tools and Chromium build system
4. Build for Android target (`target_os="android"`)
5. Package as APK or use for testing

## Requirements

- Android device with aarch64 CPU
- Root access (optional but helpful)
- Sufficient storage (~100GB+) for Chromium source and build artifacts
- Time and patience (Chromium builds take hours)

## Build Environment Ideas

On this device (Mi 9T / davinci), possible approaches:

- **proot-distro** (Debian/Ubuntu) - easier, works in userspace
- **chroot** - closer to native, may be faster
- **kexec + Linux rootfs** - run full Linux, best performance (if feasible)

## Notes

- Chromium for Android requires specific GN args and Android SDK/NDK
- Ungoogled patches need to be applied on top of Chromium source
- Building directly on Android device is slow but possible
- Cross-compilation from desktop may be easier initially

## License

This project follows Chromium and ungoogled-chromium licensing. See respective repositories for details.

## Related

- [ungoogled-chromium](https://github.com/ungoogled-software/ungoogled-chromium)
- [Chromium Android build docs](https://chromium.googlesource.com/chromium/src/+/main/docs/android_build_instructions.md)
- [postmarketOS](https://postmarketos.org/) - alternative Linux for mobile

## Building on Android (proot/chroot)

Since we're building on the device itself (aarch64):

```bash
# In proot-distro Debian/Ubuntu
apt install build-essential python3 git curl wget
# Install depot_tools
git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git
export PATH="$PWD/depot_tools:$PATH"
```

Chromium's `fetch android` and build system should work on aarch64 Linux if deps are installed.

## Next Steps

- Set up build environment
- Clone Chromium and ungoogled-chromium patches
- Test minimal build configuration
