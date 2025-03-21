# 🔲 P12 – Connect Grid Board

Now that you’ve connected the **next piece**, it’s time to update the **main board** to show the current piece falling in real time.

You’ll:
✅ Pull board and piece data from Redux  
✅ Overlay the current piece onto the board before rendering
✅ Show the game board UI based on live state

---

## 1️⃣ Update the `GridBoard` to Accept Merged Data
Open `src/components/GridBoard.js` and update it:

```jsx
import React from "react";
import GridSquare from "./GridSquare";
import "./GridBoard.css";

const GridBoard = ({ board, currentPiece }) => {
  const mergedBoard = board.map((row, r) =>
    row.map((cell, c) => ({ ...cell }))
  );

  // Overlay current piece onto the board
  if (currentPiece) {
    const { shape, color, position } = currentPiece;
    shape.forEach((row, rIdx) => {
      row.forEach((val, cIdx) => {
        if (val) {
          const r = position.row + rIdx;
          const c = position.col + cIdx;
          if (
            r >= 0 && r < mergedBoard.length &&
            c >= 0 && c < mergedBoard[0].length
          ) {
            mergedBoard[r][c] = { color };
          }
        }
      });
    });
  }

  const width = mergedBoard[0].length;
  const flatBoard = mergedBoard.flat();

  return (
    <div
      className="grid-board"
      style={{
        width: `${width * 30}px`,
        gridTemplateColumns: `repeat(${width}, 1fr)`
      }}
    >
      {flatBoard.map((square, i) => (
        <GridSquare key={i} color={square.color} />
      ))}
    </div>
  );
};

export default GridBoard;
```

✅ This overlays the current piece directly onto a copy of the board state.

---

## 2️⃣ Connect the Redux State in `TetrisGame`
Open `TetrisGame.js` and update the component:

```jsx
import { useSelector } from "react-redux";

const TetrisGame = () => {
  const board = useSelector((state) => state.game.board);
  const currentPiece = useSelector((state) => state.game.currentPiece);

  return (
    <div className="tetris-container">
      <GridBoard board={board} currentPiece={currentPiece} />
      {/* Right-side panel */}
    </div>
  );
};
```

✅ Now the board shows the current piece in its actual position.

💡 **AI Prompt:** "What’s a safe way to overlay data onto a 2D array in JavaScript?"

---

## 🧠 Stretch Challenges
- [ ] Add shadow preview of where the piece will land
- [ ] Highlight the current piece with a border or effect
- [ ] Animate the piece dropping using CSS transitions or timers

---

## ➡️ Next Step
In [P13 – Connect Controls](./13-Connect-Controls.md), we’ll finally connect the Start and Reset buttons to dispatch Redux actions and control the game!

