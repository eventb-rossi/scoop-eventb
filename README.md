# scoop-eventb

A [Scoop](https://scoop.sh) bucket for the [Event-B](https://www.event-b.org/) and
B-method tool ecosystem. This bucket is the Windows counterpart and tracks the same
versions.

It covers the command-line / JVM / native tools and the two portable GUI apps.

## Install

```powershell
scoop bucket add eventb https://github.com/eventb-rossi/scoop-eventb
scoop install eventb/<package>
```

A JDK is pulled in automatically as a dependency where needed (via the `java` bucket, which
Scoop adds on demand), so you do not need to install Java yourself.

## Packages

| Package | What it is | Notes |
|---|---|---|
| `eventb-checker` | Standalone Event-B type checker | CLI; needs Java 21 |
| `eventb-animate` | Animate Event-B models with ProB | CLI; needs Java 21 |
| `evbt` | EventBTool — code generation & documentation | CLI; needs Java 22+ |
| `rossi` | Rust toolchain for Event-B (parser, checker, CLI, LSP) | CLI; native; x64 + ARM64 |
| `b2program` | Multi-target code generator (B → Java/C++/Python/Rust/TS) | CLI; fat JAR built by this repo's CI |
| `tlc4b` | Model-check classical B via TLA+/TLC | CLI; fat JAR built by this repo's CI |
| `eventb-to-txt` | Convert Rodin Event-B models to CamilleX text | CLI; needs Python (pip-installed on demand) |
| `rodin` | Rodin Platform — Event-B IDE | Portable; Start Menu shortcut; needs Java 17+ |
| `rodin-rc` | Rodin Platform — Event-B IDE (release candidate) | Portable; Start Menu shortcut; pre-release; needs Java 17+ |
| `prob` | ProB animator / model checker (CLI `probcli` + Tcl/Tk GUI) | Portable; shim + Start Menu shortcut; Tcl/Tk runtime pulled in automatically |
| `tcltk` | Tcl/Tk 8.6 runtime (BAWT Tcl-Pure) | Dependency of `prob`; provides `tcl86.dll` and sets `SP_TCL_DSO` |
| `prob2-ui` | ProB2-UI — JavaFX animator / model checker | Portable; shim + Start Menu shortcut; needs Java 21 |
| `atelier-b` | Atelier B Community Edition — B-method IDE | Portable; Start Menu shortcut; freeware |

## Maintenance

`.github/workflows/excavator.yml` runs [Scoop's excavator](https://github.com/ScoopInstaller/GithubActions)
on a schedule to auto-bump versions and hashes (one commit per package).
`.github/workflows/ci.yml` validates manifests on pull requests.
`.github/workflows/build-fatjars.yml` rebuilds the `b2program` and `tlc4b` fat JARs from
upstream source and publishes them as release assets that those two manifests point at
(upstream publishes no usable runnable JAR).
