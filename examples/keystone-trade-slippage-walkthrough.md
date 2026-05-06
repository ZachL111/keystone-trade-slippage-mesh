# Keystone Trade Slippage Mesh Walkthrough

I use this file as a small checklist before changing the Zig implementation.

| Case | Focus | Score | Lane |
| --- | --- | ---: | --- |
| baseline | spread pressure | 121 | watch |
| stress | fill risk | 132 | watch |
| edge | portfolio drift | 110 | watch |
| recovery | quote width | 143 | ship |
| stale | spread pressure | 197 | ship |

Start with `stale` and `edge`. They create the widest contrast in this repository's fixture set, which makes them better review anchors than the middle cases.

The useful comparison is `spread pressure` against `portfolio drift`, not the raw score alone.
