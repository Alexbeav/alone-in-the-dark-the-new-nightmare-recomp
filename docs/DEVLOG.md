# Development log

## 2026-09-02: canonical multi-track Disc 1 identity

The public `v0.3.3` manifest used the merged whole-disc BIN identity, while
the setup verifier hashes Track 01. Release `v0.3.4` uses the canonical Track
01 identity and keeps the merged identity as a compatibility entry. Disc 2
keeps its separate serial and table-of-contents identity. Exact-package gates
cover both canonical discs and a wrong-disc rejection.

## 2026-09-01: deterministic Windows link

Repeated MinGW links changed 16 bytes in the product executable. The changes
included the PE timestamp and the build-ID record. Raw SHA-256 continuity was
therefore not possible.

GNU ld documents `--no-insert-timestamp` for PE targets. It states that the
option writes a zero timestamp so identical inputs can produce identical files:
<https://www.sourceware.org/binutils/docs/ld/Options.html>.

Framework commit `6b74231479230e2c4d11d3e817af5d4a7739ae0b` now applies
`--no-insert-timestamp` and an explicit content-based build ID to MinGW product
links. A source test guards both options. Two repeat-link probes produced the
same SHA-256 value. Two links from the exact package also produced SHA-256
`5B349E107BF8F2F45817455A6C124D6AC3352CAA918DCFB0F249B35A79D65D7C`.
This value replaces the stale candidate hash.

The next clean extraction changed 12 bytes. Four bytes came from `__DATE__`
and `__TIME__` in the crash identity. Those input changes also changed eight
bytes in the content-derived RSDS identifier. Framework commit `b5750bd1`
removes the volatile macros and extends the source regression to guard both
the compile input and the MinGW link options. Distinct-path clean-build proof
remains a release gate.

Two clean package builds in different extraction paths now produce SHA-256
`DCEC8403C6F290ACEED08B3D988A63036E0BB1BC342CD5946FDD65057C863D15`.
This exact value replaces all earlier candidate runtime hashes.

## 2026-09-01: v0.3.3 executable-name reconciliation

The source uses `Alone_in_the_Dark__The_New_Nightmare` for the CMake output,
code-generation setup, and package setup host. Two fresh extractions of the
initial `v0.3.3` ZIP had no build directory or executable-name marker. Both
generated from the owned Disc 1 and SCPH-5552 inputs. Both hidden builds linked
`OpenBIOS;SCPH5552` and produced runtime SHA-256
`A7C3B8AC7B8A605609473354D994334D00A2EF431BDF69A7F8C5F5A0E9AF0CD8`.
The final exact-ZIP build matched that hash. Headless startup reached frame
1934 on Disc 1 and frame 1920 on Disc 2. Both runs used SCPH-5552 and reported
no fatal event.
