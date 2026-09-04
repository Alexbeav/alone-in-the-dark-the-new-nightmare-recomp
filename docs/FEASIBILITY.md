# Alone in the Dark: The New Nightmare release feasibility

Status: `bootstrap_verified`; four-platform `v0.3.6` package pending exact-package gates

The operator confirmed that the earlier private build reaches gameplay. The
new frozen-source build also passed measured headless startup on both supported
discs with SCPH-5552: Disc 1 reached frame 693 and Disc 2 reached frame 653.

The owned European set contains `SLES-02801` and `SLES-12801`. Both discs
contain the same boot executable SHA-256,
`d93b81e7fc004a59834e14088b7cfbe6bac1ee53daa22823744b6631609743c6`.
The frozen verifier classifies the set as one program on two data images. One
setup host is valid.

The package must validate and remember both discs. Mid-session disc change is
a separate gameplay seam and remains untested. The public package must not
contain a disc, retail BIOS, generated retail code, save, prebuilt playable
executable, or private absolute path.

The `v0.3.1` setup ZIP passed its payload and startup checks, but it did not
link the SCPH-5552 backend. It failed the `PSX-BUILD-017` release gate.

The prior `v0.3.2` package passed payload and startup checks. Exact-package
Disc 1 startup reached frame 2299. Exact-package Disc 2 startup reached frame
2447. Both runs used SCPH-5552.

Two clean setup builds in different extraction paths produced identical runtime
bytes. The setup host SHA-256 is
`506e014bc043266c819a1615485c02f359cc3fb874d85dc71e1e803d1690cae6`.
The `v0.3.3` ZIP passed two fresh, spaced-path generation and build checks.
Both builds produced runtime SHA-256
`a7c3b8ac7b8a605609473354d994334d00a2ef431bdf69a7f8c5f5a0e9af0cd8`.
Both builds linked `OpenBIOS;SCPH5552`. The final exact-ZIP runtime matched
that hash. Headless Disc 1 startup reached frame 1934. Disc 2 reached frame
1920. Both runs used SCPH-5552 and reported no fatal event.

The candidate uses local framework child `b5750bd1` for deterministic build
identity. It is a child of test-registration correction `a16cc8b9` and
deterministic-link correction `6b742314`. That correction is a child of BIOS correction
`b2430fa4`. The BIOS correction is a child of CI correction `e6d054de`.
The CI correction is an additive child of frozen release base `afe9ab29`.
Publication and remote download verification are separate gates.

## v0.3.5 three-platform refresh

The candidate targets Windows x64, Linux x64, macOS Apple Silicon ARM64, and
macOS Intel x64. The setup package uses an additive framework correction that
excludes two non-SDK helpers with developer-machine paths. Each exact package
must pass the payload, setup, startup, responsiveness, and clean-exit gates on
its declared platform before publication.

## 2026-09-03 portable Linux package

The release workflow now builds Linux in a pinned Ubuntu 20.04 container.
The package gate rejects a setup host or emitter that needs a glibc version
newer than 2.31. This keeps the release compatible with the qualified Rocky
Linux 9 host. Windows and both macOS builds keep their existing runners.

## 2026-09-04 v0.3.6 POSIX setup-copy candidate

This candidate pins PSXRecomp f1d98082354641dd48750045517c23fe9ef13f34 and recomp-ui be8ac1d03ee19d55394b5a5f2d9d1506edd56659.
Linux and macOS packages use native CMake, Ninja, Python, C, and C++ tools.
Windows keeps the portable toolchain route. This change does not change game
code or the graduation state. Build-only CI and every exact-package release
gate must pass before publication.
