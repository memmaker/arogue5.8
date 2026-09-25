# Advanced Rogue 5.8 — RVIP port

Upstream: Advanced Rogue 5.8.2 (Michael Morgan, Ken Dalka), from the Roguelike
Restoration Project: https://github.com/RoguelikeRestorationProject/arogue5.8/tree/49b1289

**Our changes:** https://github.com/memmaker/arogue5.8/compare/49b1289...master
(commit 1 is the untouched upstream; everything after it is ours).

- `port:` builds on macOS/arm64 and WebAssembly: prototypes, 64-bit fixes
  (daemon arguments, 4-byte longs in saves), curses shim (`port/`) with an X11
  frontend, NetHack tiles (`port/mktiles.py`).
- `RVIP:` auto-explore (`x`), `<`/`>` walk to known stairs, Enter command
  menu, inventory with a cursor, sound events (`rvip.c` + small hooks).
- `web:` browser build (`web/build.sh`), played at https://ruzzoli.de/roguelikes/arogue58/

Build: `make arogue58-x11` (XQuartz), `./play.sh`; web: `sh web/build.sh`, `web/deploy.sh`.
Notes for the next person: `HANDOVER.md`. Process: `~/Games/RVIP.md`, `~/Games/rogue2wasm.md`.
