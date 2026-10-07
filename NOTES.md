# FOURPLAY (fourplay)

Status: runs on the reconstructed legacy engine (batch smoke test 2026-10-07: renders, takes touches). Hand play-test pending.
scoring, saved hi-score. GameId 7, 640×480. Facts: [notes/scaffold.md](notes/scaffold.md).

## Checklist
- [x] 0 unresolved symbols: all 44 loader functions it imports are in src/legacy/legacy.cpp
- [x] Board, logo, panels, instructions
- [x] Touch columns (COL0–COL6) and QUITBOX
- [x] Animations: opponent thinking/sad/happy, winner banner (delta-coded .dlt frames)
- [x] Score with thousands separator; hi-score saved (data/var/merit/highscores/7.txt)
- [ ] Sound and music confirmed by ear (three sounds come from the shared gamegraphics/misc)
- [ ] A full game to the end, both win and loss
- [ ] 2-player mode (`PLAYERS=2` in game.conf)

## Log
- 2026-10-07 — First legacy game. Decompiled fourplay.so (Ghidra, 2.2k lines) and rebuilt the
  loader API it calls from its usage: bitmaps (+4 width, +8 height), colour 5 = transparency key,
  BitmapToBitmap copies *from* (x,y) in the source, named touch zones read through
  InputCharOrDelay, SystemTimer in ms, MegacGlobals +0x24 players / +0x2038 GameId.
  Assets: gamedata/gamegraphics/fourplay (.dlt.gz + wav), language art in english/, shared
  sounds in gamegraphics/misc.
- 2026-10-07 — Played by hand. Fixed: touches were scaled twice (SDL already reports logical
  coordinates), and animations were mangled because .dlt frames after the first only hold the
  pixels that change — they are now composited. Best so far 10,595.

- 2026-10-07 — runs on src/legacy (sprite engine, gendef records, Allegro subset); smoke-tested headless.
