# Alone in the Dark: The New Nightmare knowledge report

- Date: 2026-09-02
- Retail identity: Europe `SLES-02801` and `SLES-12801`
- Architecture lane: source-only owned-input setup host
- Release target: Windows x64, Linux x64, macOS ARM64, and macOS x64; candidate version `0.3.5`

## Current state

The two-disc set is one program on two data images. The `v0.3.1` publication
preflight found a BIOS-profile mismatch. The package accepted SCPH-5552, but
it linked SCPH-1001 and started through HLE fallback.

The `v0.3.3` candidate binds the game profile, default profile, default stem,
and linked backend list to SCPH-5552. It preserves OpenBIOS as an alternate.
The final package passed its payload audit. Two fresh, spaced-path builds
linked `OpenBIOS;SCPH5552` and produced identical runtime bytes. The final
exact-ZIP runtime matched those bytes. Headless Disc 1 startup reached frame
1934. Disc 2 reached frame 1920. Both runs used SCPH-5552 and reported no fatal
event. The operator previously confirmed gameplay on the private build.
Connected in-game disc change remains open.

Release `v0.3.4` corrects the setup identity from the merged Disc 1 BIN to the
canonical split Track 01. The merged identity remains accepted. Disc 2 keeps
its existing serial and table-of-contents identity, and both owned canonical
discs are release-test inputs.

## Release controls

- Framework: 94ea3b28c1b2f10f4b0ed960145bc96d415f2c36
- Deterministic build identity: `b5750bd13fb2366a13d0cf7f06ab9584bd2fd583`
- Deterministic link correction: `6b74231479230e2c4d11d3e817af5d4a7739ae0b`
- BIOS profile correction: `b2430fa43602131b0d5c71d5d31ccf5b567f1601`
- Correction parent: `e6d054de1538881cd81dcf3592de1f561afdbb5b`
- Frozen release base: `afe9ab299aab0eeba1cc31f81bc4baf4e7fb2ab7`
- Recomp-UI: `4eda65430a431e5685ae0c515ebcd912c7843bff`
- RetComM Studio: `249422969c1c59ac2a1f8aa2299e876a7133998e`
- Distribution: owned input only
- Platform claim: pending exact-package gates on all four targets

## Open gates

1. Bind publication authorization to the exact release manifest.
2. Create and audit the private release draft.
3. Redownload and verify the exact remote bytes.
4. Complete a natural connected disc-change route.

## Corpus consulted

The release work uses `PSX-BUILD-017`, `PSX-DISC-001`, `PSX-PUB-004`,
`PSX-PUB-006`, `PSX-WIN-005`, `PSX-WIN-006`, and the release regression
ledger.

## v0.3.5 three-platform refresh

The source now binds the package-only privacy correction and targets Windows
x64, Linux x64, macOS ARM64, and macOS x64. The replacement build-only CI,
complete archive audit, and native package gates remain required. This source
change does not publish a release or claim platform support.
