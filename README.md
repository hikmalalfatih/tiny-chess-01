# tiny-chess-01 entry

A chess engine in a single `main.py` (<= 4,096 bytes), Python stdlib only.
It plays through the make.fun environment protocol (POST /game, /move,
/resign) and picks every move from a fixed node budget — no wall clock
anywhere, so replays reproduce byte-for-byte.

Design: 0x88 board, pseudo-legal move generation with make/unmake, negamax
alpha-beta with PVS, iterative deepening, transposition table, null-move
pruning, late-move reductions, check extensions and a quiescence search
(captures, promotions, check evasions). Move ordering: TT move, MVV-LVA,
killers, history. Evaluation is incremental: material + piece-square
tables (string-encoded, middlegame/endgame king blend), bishop pair,
doubled/isolated pawn penalties; repetition and the 50-move rule score
as draws inside the search.

`main.py` is produced by the kit's `makefun compress` from the entry
source. Local practice on the kit's three 6-game trials: Elo 1809,
1451 and 1279 (mean 1513; house baseline mean 1365).
