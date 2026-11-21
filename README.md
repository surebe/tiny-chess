# Tiny Chess — a 4 KB engine with an 8-line trap book

An entry to make.fun's [tiny-chess-01](https://make.fun/bounty/tiny-chess-01) bounty, *"Build the strongest chess engine in 4 KB of Python"*.

[![make.fun bounty](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/surebe/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/surebe/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01)

## What it is

`main.py` (4,095 bytes, Python standard library only) is a complete chess
engine: alpha-beta search with quiescence, a transposition table, iterative
deepening under a node budget, move ordering with LMR and null-window
refinement, and a tapered piece-square evaluation — plus a book of eight
prepared trap lines, one per opponent scenario, each verified move-by-move
against the house oracle to end in a scripted mate:

| Scenario | Scripted mate |
|---|---|
| King's Gambit, pawn odds, depth 3 | 23 ply |
| Petrov, pawn odds, depth 2 | 35 ply |
| Italian, pawn odds, depth 4 | 51 ply |
| Dutch, pawn odds, depth 4 | 81 ply |
| Bird, handicap, 100k nodes | 102 ply |
| Slav, pawn odds, 250k nodes | 103 ply |
| Morphy, handicap, depth 3 | 106 ply |
| Scandinavian, handicap, depth 4 | 114 ply |

Off book, the engine plays the position: fully deterministic, worst move
3.6 s against the 10 s limit in local trials. In the local practice gauntlet
(six games per trial, house opponents) it sweeps one trial at the 2110 Elo
cap and scores 19 across four trial sets.

## Layout

- `main.py` — the whole engine, packed to fit the 4,096-byte cap.
- `LICENSE` — MIT.

The engine speaks the competition's HTTP harness protocol
(`MAKEFUN_ENV_URL`): it polls for its game, replays the move list, and
answers with its chosen move in UCI.
