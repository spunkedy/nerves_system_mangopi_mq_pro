# Changelog

This project does NOT follow semantic versioning. The version increases as
follows:

1. Major version updates are breaking updates to the build infrastructure.
   These should be very rare.
2. Minor version updates are made for every major Buildroot release. This
   may also include Erlang/OTP and Linux kernel updates. These are made four
   times a year shortly after the Buildroot releases.
3. Patch version updates are made for Buildroot minor releases, Erlang/OTP
   releases, and Linux kernel updates. They're also made to fix bugs and add
   features to the build infrastructure.

## v0.1.1

The release fixes some issues that made v0.1.0 hard to use. The flaky MMC boot
issue is still present. If your board hits it, unplugging and replugging in the
MicroSD card has been found to be a more reliable workaround than rebooting.

* Updates
  * Enable the RISC-V vector extension

* Fixes
  * Fix compilation warnings when using C standard headers. If a library had
    `-Werror`, these would end up breaking Elixir libraries that had C/C++ code.
  * Make sure that the watchdog is active during boot and can't be disabled.
    This recovers (with a reboot) from some more hangs.

## v0.1.0

This is the initial release.
