# Advanced Rogue 5.8 — RVIP handover (2026-09-25)

Ported right after Advanced Rogue 7.7 (`~/Games/arogue7.7`, read its
HANDOVER first); same shim, frontends, `rvip.c` and web files.

- `struct delayed_action.d_arg` was an `int`; `doctor` gets `&player`.
  Now a `long`; `daemon()`/`fuse()` take `void *`; on restore doctor's
  argument is set back to `&player` (the save keeps 4 bytes).
- `rs_read_long/ulong`: 4-byte read into 8-byte long (experience showed
  garbage after restore). Fixed as in 7.7.
- `save_file()` takes a `FILE *` here (7.7: an fd): `port/be_web.c` is the
  XRogue version.
- No C_* command names and no `lines`/`cols` globals: `rvip.c` defines the
  keys itself and uses LINES/COLS. The shim gained `wgetnstr()`.
- 4 classes (fighter, magician, cleric, thief): `CLASS` in `port/mktiles.py`.
- Testing: paths over 80 characters break the save file name (`LINELEN`);
  run tests from a short directory with `HOME=save`.
- Prompt line (RVIP step 5 / W4, 2026-09-26): the live message row is shown in a
  box over the map by `RvipWM.prompt` (rvip-wm.js). A key hides it only while
  the game waits for a command, so a question stays up until answered.
  Here: `be_prompt(r)` from `msg_refresh()` in `port/wcurses.c` (row 0 text),
  `js_key(wc_cmd_prompt)` in `port/be_web.c`; `be_x11.c` has an empty stub.
