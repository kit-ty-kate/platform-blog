title: "opam releases: 2.0.10, 2.1.1 & opam depext 1.2!"
authors: [
  "Raja Boujbel - OCamlPro" {"mailto:raja.boujbel(à)ocamlpro.com"}
  "Louis Gesbert - OCamlPro" {"mailto:louis.gesbert(à)ocamlpro.com"}
]
date: "2021-11-10"
--BODY--

<!--
_Feedback on this post is welcomed on [Discuss](https://discuss.ocaml.org/t/XXXXXX)!_
-->

We are pleased to announce several minor releases: [opam 2.0.10](https://github.com/ocaml/opam/releases/tag/2.0.10), [opam 2.1.1](https://github.com/ocaml/opam/releases/tag/2.1.1), and [opam-depext 1.2](https://github.com/ocaml-opam/opam-depext/releases/tag/1.2).

Opam releases version contain backported fixes, while `opam-depext` has been adapted to be compatible with opam 2.1 (which has depexts as builtin) to smooth some user experience when switching from 2.0 to 2.1.

## [opam-depext 1.2]()
 Integrates opam calls for handling external dependencies (check, install). If opam 2.1 is used, opam-depext will use the builtin opam depext commands instead.
 Use of opam-depext with opam 2.1 is still discouraged given its structural issues and the new builtin 2.1 commands are highly recommended.

On the 2.0 side:
* Force yum-based distributions to not upgrade when updating [[#137](https://github.com/ocaml-opam/opam-depext/pull/137) @kit-ty-kate]
* Archlinux: always upgrade all the installed packages when installing a new package [[#138](https://github.com/ocaml-opam/opam-depext/pull/138) @kit-ty-kate]

## [opam 2.0.10](https://github.com/ocaml/opam/blob/2.0.10/CHANGES)
* Fix reverting environment additions to PATH-like variables when several dirs added at once [[#4861](https://github.com/ocaml/opam/pull/4841) @dra27]
* Ensure setenv can use package variables defined during the build [[#4841](https://github.com/ocaml/opam/pull/4841) @dra27]

## [opam 2.1.1](https://github.com/ocaml/opam/blob/2.1.1/CHANGES)
### Switch
* Put back support for switch creation with packages argument and `--packages` option with cli 2.0, e.g. `opam switch create . 4.12.0+options --packages=ocaml-option-flambda` [[4853](https://github.com/ocaml/opam/issues/4853) @rjbou]
* Fix `set-invariant`: default repos were loaded instead of switch repos [[4869](https://github.com/ocaml/opam/pull/4869) @rjbou]

### External dependencies

* Homebrew: add support for casks and full-names [[4801](https://github.com/ocaml/opam/pull/4801]) @kit-ty-kate]
* Archlinux: handle virtual package detection [[4833](https://github.com/ocaml/opam/issues/4833) @rjbou]
* Disable the detection of available packages on RHEL-based distributions. This fixes an issue on RHEL-based distributions where yum list used to detect available and installed packages would wait for user input without showing any output and/or fail in some cases [[4791](https://github.com/ocaml/opam/issues/4791) @kit-ty-kate]

### Sandbox
* Run the sandbox check in the temporary directory [[4787](https://github.com/ocaml/opam/issues/4787) @dra27]

### System
* OpamSystem: avoid calling Unix.environment at top level [[4789](https://github.com/ocaml/opam/issues/4789) @hannes]
* the opam 2.0.10 fixes (see above)

### opam build
* Fix the cold target in presence of an older OCaml compiler version on macOS [[4802](https://github.com/ocaml/opam/pull/4802)]
* Fix vendored build on mingw-w64 with g++ 11.2 [[4835](https://github.com/ocaml/opam/pull/4835)]

---

Opam installation instructions (unchanged):

1. From binaries: run

    ```
    bash -c "sh <(curl -fsSL https://raw.githubusercontent.com/ocaml/opam/master/shell/install.sh) --version 2.1.1"
    ```

    or download manually from [the Github "Releases" page](https://github.com/ocaml/opam/releases/tag/2.1.1) to your PATH. In this case, don't forget to run `opam init --reinit -ni` to enable sandboxing if you had version 2.0.0~rc manually installed or to update you sandbox script.

2. From source, using opam:

    ```
    opam update; opam install opam-devel
    ```

   (then copy the opam binary to your PATH as explained, and don't forget to run `opam init --reinit -ni` to enable sandboxing if you had version 2.0.0~rc manually installed or to update your sandbox script)

3. From source, manually: see the instructions in the [README](https://github.com/ocaml/opam/tree/2.1.1#compiling-this-repo).

We hope you enjoy this new minor version, and remain open to [bug reports](https://github.com/ocaml/opam/issues) and [suggestions](https://github.com/ocaml/opam/issues).
