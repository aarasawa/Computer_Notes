#Shogi
### Shogi Board and Pieces

The Shogi board is a 9x9 grid. Each player has 20 pieces, arranged as follows:

- **Pawns (9 per player)**: These are placed on the third row from each player.
- **Lances (2 per player)**: Placed on the corners of the board (a1, i1 for one player and a9, i9 for the other).
- **Knights (2 per player)**: Placed next to the lances (b1, h1 for one player and b9, h9 for the other).
- **Silver Generals (2 per player)**: Placed next to the knights (c1, g1 for one player and c9, g9 for the other).
- **Gold Generals (2 per player)**: Placed next to the silver generals (d1, f1 for one player and d9, f9 for the other).
- **Bishops (1 per player)**: Placed on the same row as the generals (b2 for one player and b8 for the other).
- **Rooks (1 per player)**: Placed on the same row as the generals (h2 for one player and h8 for the other).
- **King (1 per player)**: Placed in the center of the back row (e1 for one player and e9 for the other).

### Initial Setup Diagram

```
9  a  b  c  d  e  f  g  h  i
----------------------------
1 | L  N  S  G  K  G  S  N  L |
2 |    R               B    |
3 | P  P  P  P  P  P  P  P  P |
4 |                           |
5 |                           |
6 |                           |
7 | p  p  p  p  p  p  p  p  p |
8 |    b               r    |
9 | l  n  s  g  k  g  s  n  l |
----------------------------
```

- Uppercase letters represent one player's pieces.
- Lowercase letters represent the opponent's pieces.
- `P` for Pawn, `L` for Lance, `N` for Knight, `S` for Silver General, `G` for Gold General, `B` for Bishop, `R` for Rook, and `K` for King.

### Basic Rules

1. **Objective**: The objective is to capture your opponent's King.
2. **Moves**:
   - **King**: Moves one square in any direction.
   - **Gold General**: Moves one square in any direction except diagonally backward.
   - **Silver General**: Moves one square in any direction except directly sideways or backward.
   - **Knight**: Moves in an "L" shape (two squares forward and one square sideways).
   - **Lance**: Moves any number of squares forward.
   - **Bishop**: Moves any number of squares diagonally.
   - **Rook**: Moves any number of squares horizontally or vertically.
   - **Pawn**: Moves one square forward.

3. **Promotion**: When a piece moves into, out of, or within the opponent's promotion zone (the last three rows), it can be promoted. Promotion changes how the piece moves:
   - **Pawn, Lance, Knight, Silver General**: Promote to Gold General.
   - **Rook**: Promotes to Dragon King (moves like a Rook plus one square diagonally).
   - **Bishop**: Promotes to Dragon Horse (moves like a Bishop plus one square orthogonally).

### Promotion Zone Diagram

```
Promotion zone (for each player):
----------------------------
7 | p  p  p  p  p  p  p  p  p |
8 |    b               r    |
9 | l  n  s  g  k  g  s  n  l |
----------------------------
```

### Dropping Captured Pieces

Captured pieces can be returned to the board as your own pieces. They are placed on any empty square and regain their original movement abilities.

### Example of a Move and Promotion

1. Move a pawn forward from `7f` to `7e`:
   ```
   Original:
   7 | p  p  p  p  p  p  p  p  p |
   Move:
   7 | p  p  p  p  p  p  p  -  p |
   6 | -  -  -  -  -  -  -  p  - |
   ```

2. If the pawn reaches `9e`, it can promote:
   ```
   Promoted Pawn (`to` for tokin, promoted pawn):
   9 | l  n  s  g  k  g  s  n  L |
   ```

### Winning the Game

You win the game by placing your opponent's King in checkmate, a position where it cannot escape capture.

### Diagram of Checkmate

If the King is at `9e`, a Rook at `9d` and a promoted pawn at `8e` can create a checkmate:
```
9 | l  n  s  G  K  g  s  n  l |
8 |    b  r           to    |
```