# tiny-chess-01 v2: 4 KB chess engine (PVS + LMR)

A 0x88 alpha-beta engine in 4,096 bytes of Python (packed with the kit's
`makefun compress` from the readable `engine.py` kept beside the repo).

- Iterative deepening to a fixed 120,000 nodes a move (never a clock),
  so every trial replays move for move.
- Principal Variation Search + Late Move Reductions (1 ply, late quiet
  moves only, never when in check); transposition table, killer moves,
  null-move pruning (R=3).
- Quiescence over captures, promotions and replies to checks, with
  delta pruning.
- Material + piece-square tables (Michniewski), tapered king tables,
  bishop-pair bonus; repetition inside the search scores 0.
- Talks to the env only: POST /game, /move; no model calls.

Local grade (kit env server, official scorer, practice trial-1):
- v1 (this engine's predecessor): 4 won, 2 drawn, 0 lost — Elo 1654.
- v2 (this packed main.py): 5 won, 1 drawn, 0 lost — Elo 1809,
  spare plies 393. Beats v1 by +155 Elo.
Practice floor is 1,154; the house baseline (sunfish 4 KB) rates ~1,365.
