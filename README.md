# OP_KSUN_FS

KernelSU Next + SUSFS kernels for OnePlus devices on stock OxygenOS / ColorOS 14, 15 and 16, built on GitHub Actions from [OnePlus kernel sources](https://github.com/OnePlusOSS).

This is a fork of [OP_KSUN_FS by SakFi](https://github.com/sakfi/OP_KSUN_FS), and most of it is his work: the build workflows, device configs, kernel patch set, LKM packaging with on-device `ksud boot-patch`, the SUSFS guard module and the [AnyKernel3.1 installer](https://github.com/sakfi/AnyKernel3.1). This fork adds pinned builds for the OnePlus 11 and small fixes. If you want builds for other devices, or the original project, go to [SakFi's repo](https://github.com/sakfi/OP_KSUN_FS) ([Telegram](https://t.me/SakFi)). The `SKF_` zip prefix and the `SakFi-OP` kernel name are his and are kept.

For LineageOS, use [LineageOS_KSUN_SUSFS](https://github.com/fishing-agents/LineageOS_KSUN_SUSFS) instead.

## Releases

[Latest release](https://github.com/fishing-agents/OP_KSUN_FS/releases/latest). Current build:

- **OnePlus 11 (salami)**, OxygenOS 16, `android13-5.15.197`, KernelSU Next v3.4.2, SUSFS v2.3.0: `SKF_OP11_A16_android13-5.15.197_KSUN_33355_SuSFS_v2.3.0.zip`

Zip names follow `SKF_{MODEL}_{OS}_{KERNEL}_{KSU}_{KSU_VERSION}_SuSFS_{SUSFS_VERSION}.zip`. A `.sha256` file is published next to each zip.

Other devices have configs under [`configs/`](configs/) (`a14`, `a15`, `a16`) and can be built from the workflow, but only the releases above are published here. See [compatibility.md](compatibility.md).

## What's in the kernel

- **KernelSU Next**, as a loadable module (LKM, default) or built in (`ksu_mode: builtin`). In LKM mode the installer patches `init_boot` (or `boot`) with `ksud boot-patch` during flashing.
- **SUSFS** with `SUS_PATH`, `SUS_MOUNT`, `SUS_KSTAT`, `SUS_MAP`, `SPOOF_UNAME`, `SPOOF_CMDLINE`, `OPEN_REDIRECT`, `AVC_SPOOF`.
- Extras: NTSync, BBRv3, WireGuard, TTL / IP set, Baseband Guard, MGLRU and scheduler tuning, Droidspaces container support.
- Packaged with SakFi's AnyKernel3.1 (based on osm0sis's AnyKernel3).

## Install

Requirements: unlocked bootloader, and a copy of the stock `boot.img` and `init_boot.img` of the installed build (for rescue).

1. Check that the release matches your device and OxygenOS major version. Don't flash a zip after a major OTA (for example A15 to A16) until it's confirmed for the new version.
2. Flash the zip with [Kernel Flasher](https://github.com/fatalcoder524/KernelFlasher), [Horizon Kernel Flasher](https://github.com/libxzr/HorizonKernelFlasher) or a custom recovery.
3. Reboot, then install the [KernelSU Next manager](https://github.com/KernelSU-Next/KernelSU-Next/releases) and the [SUSFS module](https://github.com/sidex15/ksu_module_susfs/releases).

Rescue: flash the stock `boot.img` and `init_boot.img` from fastboot.

Play Integrity, attestation and the full ColorOS to OxygenOS to LineageOS path are covered in [oneplus-coloros-oos-lineageos](https://github.com/fishing-agents/oneplus-coloros-oos-lineageos).

## Building

Run the `build-kernel-release.yml` workflow from the Actions tab and pick the device config. Builds run only on GitHub Actions.

## Disclaimer

Flashing a kernel that doesn't match the installed firmware can bootloop the phone or lose data. You flash at your own risk.

## Credits

- [SakFi](https://github.com/sakfi): author of [OP_KSUN_FS](https://github.com/sakfi/OP_KSUN_FS), which this fork is based on (build suite, configs, LKM packaging, SUSFS guard, [AnyKernel3.1](https://github.com/sakfi/AnyKernel3.1))
- [fatalcoder524](https://github.com/fatalcoder524) and [WildKernels](https://github.com/WildKernels/OnePlus_KernelSU_SUSFS): original OnePlus pipeline
- [KernelSU Next](https://github.com/KernelSU-Next/KernelSU-Next) (rifsxd)
- [SUSFS](https://gitlab.com/simonpunk/susfs4ksu) (simonpunk), [SUSFS module](https://github.com/sidex15/ksu_module_susfs) (sidex15)
- [AnyKernel3](https://github.com/osm0sis/AnyKernel3) (osm0sis)
- [Droidspaces](https://github.com/ravindu644/Droidspaces-OSS) (ravindu644)
