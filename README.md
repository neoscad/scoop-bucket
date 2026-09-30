# Scoop bucket for NeoSCAD

[NeoSCAD](https://neoscad.org) is an OpenSCAD-compatible programmable solid
CAD. This bucket installs its command-line program, `neoscad` (with its
`serve`, `mcp` and `lsp` subcommands), on Windows x86_64 and ARM64.

## Install

```powershell
scoop bucket add neoscad https://github.com/neoscad/scoop-bucket
scoop install neoscad
```

Then `neoscad --help`. `scoop update neoscad` moves to a newer release.

## Where the manifest comes from

`bucket/neoscad.json` is written by NeoSCAD's release workflow
([neoscad/neoscad](https://github.com/neoscad/neoscad)) when a release's
Windows zips are published: it is filled from the template
`packaging/scoop/neoscad.json` there with the release's version and SHA-256
checksums. Change the template, not this file; a hand edit here is
overwritten by the next release.

## Unsigned builds

The Windows builds are not Authenticode-signed. Installing through Scoop
does not show SmartScreen's prompt, but Windows 11's Smart App Control, where
it is enabled, may still block an unsigned program.

Scoop checks each download against the SHA-256 in the manifest. To check
where a file came from, download it from the
[release](https://github.com/neoscad/neoscad/releases) and verify its GitHub
artifact attestation with the [GitHub CLI](https://cli.github.com):

```powershell
gh attestation verify neoscad-cli-x86_64-pc-windows-msvc.zip -R neoscad/neoscad
```

(`neoscad-cli-aarch64-pc-windows-msvc.zip` on ARM64.) It succeeds only for a
file built by NeoSCAD's release workflow in that repository.

## Licence

NeoSCAD is GPL-2.0-or-later. The zip carries its `LICENSE`, `NOTICE` and
the licences of what the program embeds.
