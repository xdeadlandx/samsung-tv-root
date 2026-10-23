# Q70T research — P00 baseline (2026-10-23)

> Scope: owner-authorized research on a **candidate** Samsung Q70T (2020). No model/firmware or runtime is confirmed from the physical TV yet. This note is **not** a compatibility claim or an exploit procedure.

## Upstream baseline

- Upstream: `chris-ritsen/samsung-tv-root`; fork: `xdeadlandx/samsung-tv-root`.
- Fork branch point: `3b97edf3762db7670585d73e29623dc56195bf98` (`master`, matching upstream on 2026-10-23).
- Project package at this baseline: `0.0.12`; Python >=3.12.
- Project code: `src/samsung_tv_root/`; test suite: `tests/`; build pipeline: `.github/workflows/build.yml`.
- Exploit-specific compatibility profiles: `compatibility.py` (QN90B and QN90F); generic, *runtime-dependent* archive route: `archive_root.py`.

## Evidence levels

1. **Known from project conversation:** user believes the target is a Samsung Q70T; previous notes identify a possible `QN65Q70TAGXZS`. Reconfirm against the device's on-screen model code.
2. **Not yet observed:** TV firmware/build string, Tizen release, CPU architecture, kernel, SDK daemon reachability, runtime/.NET availability and package capabilities.
3. **Not demonstrated:** SDK injection foothold, archive-launcher compatibility, root privileges, UEP changes, persistence or any custom Q70T feature.
4. Firmware published online for a model or region is **not evidence** that this TV runs it.

## Plan and release gates

| Gate | Activity | Allowed at this stage |
|---|---|---|
| P00 | Fork provenance, code inventory, offline test baseline and safety boundaries | Documentation and host-only static checks |
| P01 | Record exact model and firmware from on-TV UI (redact serials, MAC, IP, tokens) | Manual reads; no TV exploits |
| P02 | Build a Q70T evidence matrix: architecture, Tizen version, known upstream requirements and safe diagnostics | Offline analysis and owner-reviewed, read-only observations |
| P03 | Assess exploit feasibility against exact build; document expected failure modes and recovery conditions | No live root attempt without explicit owner authorization |
| P04 | If P03 supports a test, design one bounded trial with evidence capture and rollback | Separate approval before live exploitation |
| P05 | Feature experiments (privacy, services, remote integration) | Only after repeatable root proof and individually reviewed changes |

## Important safety distinction

- `samsung-tv-root doctor` checks the **host installation**, SDB discovery and payload files; it is *not* a proof of TV compatibility.
- Existing `preflight` commands can exercise the SDB command-injection foothold; they are **not guaranteed read-only** merely by being called preflight.
- **`archive-root probe` is an actual root attempt:** it stages files, starts a privileged callback and performs cleanup; it must never be presented as a passive inventory test.
- Until target identity and firmware are confirmed: **do not run** root commands, archive-root probe, UEP toggles, firmware writes, uninstall/debloat, persistence changes or region changes.
- Keep all TV research on a trusted private LAN. Do not publish device identifiers, tokens, credentials, full command logs or firmware-derived secret material.
- Never claim support solely from a Q70T series name or a neighboring model's successful exploit.

## Next evidence requested

From **Settings > Support > About This TV**, record only:
- Exact model code (no serial number).
- Software version / firmware build.
- Tizen version if shown.

Then compare these data to upstream requirements **before** implementing or testing a new profile. Keep `master` available for upstream synchronization; use feature/research branches and reviewed PRs for local changes.
