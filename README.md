[![make.fun](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/bocahtamvan/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/bocahtamvan/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01)

# Tiny Chess

The strongest chess engine I can fit in 4,096 bytes of Python, built for the
[make.fun tiny-chess-01 bounty](https://make.fun/bounty/tiny-chess-01).

`main.py` is the whole engine: a 0x88 alpha-beta searcher with PVS, a
transposition table, null-move pruning, killer and history move ordering,
MVV-LVA capture ordering, quiescence over captures and promotions (and every
reply to a check), and a material + piece-square + passed-pawn + king-shield
evaluation. It searches to a fixed node budget per move, never a clock, so
every trial replays move for move.

It plays the house gauntlet through the env at `MAKEFUN_ENV_URL`:
`POST /game` serves the game in play, `POST /move` plays a move, and the loop
ends when the env answers `status: "done"`.

## Run it

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:8080 python3 main.py
```

## Build it

The entrypoint is packed with the kit's `makefun compress` from the readable
source in `src/engine.py` (kept out of the committed snapshot):

```sh
node <kit>/cli/makefun.mjs compress src/engine.py --out main.py
```
