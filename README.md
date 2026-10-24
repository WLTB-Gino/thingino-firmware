# Issue #1862 — crash evidence photos

Photos of the SSH session (reporter's camera: Tapo C200C, T23N, prudynt-t 6e48034, firmware ciao e260f09e8) during a foreground run with stderr visible. Captured 2026-10-25, before the crash report in /tmp was lost to a reboot.

## 01-crash-banner-foreground-run.jpg
Crash banner + pre-crash timeline:
- `Prudynt crashed! Crash report saved to /tmp/prudynt_crash.log`
- `Signal: SIGSEGV (Segmentation fault) at address 0x8`
- Client 192.168.50.200: OPTIONS -> digest auth -> DESCRIBE -> SETUP x3 -> PLAY
- `Backchannel activated via PLAY`, `Audio codec=AAC rate=16000 pt=97`, `ch0 prepending SPS/PPS to frame` ~0.5s before death

## 02-crash-report-registers-stack.jpg
Start of the crash report body:
- `prudynt-t unknown (Oct 16 2026 10:34:52)`, PID 1009
- SIGSEGV, fault address 0x8
- PC 0x778fb6e4, SP 0x74598c68, RA 0x778fb5d8 + full MIPS GPR dump
- Stack hexdump (256 bytes from SP)
- `Text addresses on stack (2KB scan)` — return-address candidates (poor-man's backtrace)

## 03-crash-report-tail-end.jpg
Tail of the same dump: remaining registers (s4-s7, t8/t9, k0/k1, gp/sp/fp/ra), stack hex, text-address scan, `=== END CRASH REPORT ===`.

Note: photos 02/03 were taken of the SAME crash report; the report file itself was lost to an unrelated reboot before it could be cat'd as text. Sequence is what matters, not timestamps (camera has no battery RTC).
