# FM experiment inputs (not installed by vendor makefiles)

These files are diagnostic inputs, not a working FM release.
The normal proprietary/vendor/firmware files remain unchanged.

stock-wmt-01.06.000 contains the two MT6630 E3 patch files extracted from
TAB-A04-BR3 Android 7.0 system/vendor/firmware, build 01.06.000 (2020-07-20).
Their embedded build timestamp is 20190702b001007. The normal Android 10
BSP blobs have embedded timestamp 20200515b001007. Header platform/HW/SW
and patch addresses match; that alone does not establish compatibility.

dsp contains the V1/V2 receive patch/coeff and configuration already used
on the test device. These were preserved from the prior FM investigation;
they are not claimed to be shipped by Benesse. TX firmware is not included.
All files are binary-identical copies, not binary patches. SHA256SUMS
identifies the exact inputs. Retain original firmware and its permissions,
SELinux contexts, and hashes before any experiment, and restore afterwards.

The kernel branch fm-autonomous-20261019 supplies tools/a04br3/build-fm.sh
and fm-test.c. No AOSP or reference BSP source modification is required.
Only use an idle, rooted test device with UART and known boot recovery.
WMT patches are loaded during combo initialization; reboot after replacement.
Do not interpret successful WMT initialization or a tune return code as
proof of actual FM reception.

## Observed A/B result (2026-10-19)

On the same USB-fixed #18 kernel and traced FM module, the 2019 stock
patch pair completed combo initialization and both patch downloads.
FM POWERUP still returned 1005, with the same raw event sequence:
`04 22 02 00 e8 03 04 07 00 00`. No reception was demonstrated.
The 2020 BSP patch pair was restored and its hashes checked before reboot.
This rules out that specific substitution as a fix; it does not establish
hardware omission or rule out every firmware/clock/power issue.
