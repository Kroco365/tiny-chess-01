[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/Kroco365/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/Kroco365/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

# tiny-chess-01: a compact chess engine in 4 KB of Python

A chess engine that plays the house gauntlet of
[make.fun's tiny-chess-01](https://make.fun/bounty/tiny-chess-01)
through the contest env. `main.py` is the whole engine: at most 4,096
bytes as committed, Python 3.13, standard library only.

## Design

- Negamax with alpha-beta pruning and iterative deepening to a fixed
  budget of 150,000 nodes a move — never a clock, so every trial replays
  move for move.
- Quiescence search over captures and promotions, plus every reply
  while in check.
- Transposition table, killer moves and MVV-LVA capture ordering.
- Evaluation: material plus piece-square tables (with a separate
  endgame king table), a bishop-pair bonus, and a draw score for
  insufficient material.
- `main.py` is a packed entrypoint: an LZMA payload of the readable
  source (`engine.py`, kept beside the entry and sent with the
  transcripts) with its unpacker. The payload and the unpacker are both
  part of its 4,096 bytes.

## Size

- `main.py`: 3,217 bytes (packed).
- The whole tree is at most 8,192 bytes; no file is over 4,096.
- License: MIT (see LICENSE).
