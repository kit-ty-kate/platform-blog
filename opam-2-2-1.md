title: "opam 2.2.1 release"
authors: [
  "Raja Boujbel - OCamlPro" {"mailto:raja.boujbel(à)ocamlpro.com"}
  "Kate Deplaix - Ahrefs" {"mailto:kit-ty-kate(à)outlook.com"}
  "David Allsopp - Tarides" {"mailto:david(à)tarides.com"}
]
date: "2024-08-22"
--BODY--

_Feedback on this post is welcomed on [Discuss](https://discuss.ocaml.org/t/ann-opam-2-2-1-release/XXXXX)!_

We are pleased to announce the release of opam 2.2.1.

We've fixed a couple of regressions and would like to encourage users of opam 2.2 to upgrade.

## Changes

The three main changes are:

* Fix a regression in `opam install --deps-only` where the direct dependencies were not set as root packages
  (spotted in the wild by @rjbou and also [reported on Discuss](https://discuss.ocaml.org/t/how-to-list-all-root-dependencies-in-the-current-switch/15142))
* Fix a regression when fetching git packages where the resulting git repository could lead to unexpected outputs of git commands, by disabling shallow clone by default except when fetching an opam repositories
  ([#6145](https://github.com/ocaml/opam/issues/6145))
* Mitigate [curl/curl#13845](https://github.com/curl/curl/issues/13845) by falling back from `--write-out` to `--fail`
  if exit code 43 is returned by curl. In particular, this fixes `opam init` when run from cmd/PowerShell on Windows 11 23H2
  ([#6120](https://github.com/ocaml/opam/issues/6120))

A couple more improvements and additions to the testsuite were made.
You can view the full list of changes in the [release note](https://github.com/ocaml/opam/releases/tag/2.2.1).

## Try it!

The upgrade instructions are unchanged:

1. Either from binaries: run

For Unix systems
```
bash -c "sh <(curl -fsSL https://raw.githubusercontent.com/ocaml/opam/master/shell/install.sh) --version 2.2.1"
```
or from PowerShell for Windows systems
```
Invoke-Expression "& { $(Invoke-RestMethod https://raw.githubusercontent.com/ocaml/opam/master/shell/install.ps1) }"
```
(or via `winget upgrade OCaml.opam`) or download manually from [the Github "Releases" page](https://github.com/ocaml/opam/releases/tag/2.2.1) to your PATH.

2. Or from source, manually: see the instructions in the [README](https://github.com/ocaml/opam/tree/2.2.1#compiling-this-repo).


You should then run:
```
opam init --reinit -ni
```


Please report any issues to [the bug-tracker](https://github.com/ocaml/opam/issues).

Happy hacking!