# tiny-chess-01 — v2 (submission)

A chess engine in 4 KB of Python for the `tiny-chess-01` make.fun bounty:
"Build the strongest chess engine in 4 KB of Python."

`main.py` (3,265 bytes) is the whole engine. `v2-submit.py` is the readable source
it was packed from (`makefun compress v2-submit.py`).

## Engine

- 0x88 board, incremental Zobrist hash, alpha-beta with null-move pruning and LMR
- Tapered eval: midgame + endgame piece-square tables interpolated by game phase
- Transposition table (reset per move) and killer moves
- Repetition = draw (threefold / fifty-move), standard
- Fixed node cap (120,000 nodes/move) — deterministic, no clock, no randomness

## Results (practice, 6-game trial-0, fresh kit)

| engine | Elo | W/D/L | wall |
|---|---|---|---|
| v2 (this submission) | 1,451 | 3 / 2 / 1 | 1,140 s |
| v4 (PVS + aspiration + gated repetition) | 876 | 1 / 0 / 5 | 850 s |
| v5 (PeSTO eval on v2's search) | 1,191 | 2 / 1 / 3 | 1,195 s |

v2 is the strongest of the three builds measured on the same trial-0: it beats the
depth-2, depth-4 and nodes-250k engines, draws depth-3 and nodes-100k, and only
loses to nodes-500k.

Sunfish baseline on the same 6-game set: ~1,365. Floor to enter the final: 1,154.

## Layout

- `main.py` — the engine (packed, ≤ 4,096 bytes)
- `v2-submit.py` — the readable source
- `LICENSE` — MIT

## Build

```sh
node <kit>/cli/makefun.mjs compress v2-submit.py   # v2-submit.py -> main.py
```

## License

MIT. See `LICENSE`.
