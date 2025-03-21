# 🔗 P11 – Connect Next Block

Now that we have defined block shapes and a random generator, it's time to wire the **NextBlock** preview UI to display actual randomly selected pieces from Redux.

You’ll:
✅ Use `useSelector` to pull `nextPiece` from Redux state  
✅ Render its shape in the `NextBlock` component

---

## 1️⃣ Update `NextBlock.js` to Handle Shape and Color
Open `src/components/NextBlock.js` and update it:

```jsx
import React from "react";
import GridSquare from "./GridSquare";
import "./GridBoard.css";

const NextBlock = ({ piece }) => {
  const grid = Array(4).fill(null).map(() => Array(4).fill({ color: "#000" }));

  piece.shape.forEach((row, r) => {
    row.forEach((cell, c) => {
      if (cell) grid[r][c] = { color: piece.color };
    });
  });

  const flatGrid = grid.flat();

  return (
    <div
      className="grid-board"
      style={{
        width: "120px",
        gridTemplateColumns: `repeat(4, 1fr)`
      }}
    >
      {flatGrid.map((cell, i) => (
        <GridSquare key={i} color={cell.color} />
      ))}
    </div>
  );
};

export default NextBlock;
```

✅ This renders the next block into a fixed 4x4 grid.

---

## 2️⃣ Pull State from Redux in `TetrisGame`
Open `TetrisGame.js` and use the real `nextPiece` from state:

```jsx
import { useSelector } from "react-redux";

const TetrisGame = () => {
  const nextPiece = useSelector((state) => state.game.nextPiece);

  return (
    <div className="tetris-container">
      {/* other UI */}
      <NextBlock piece={nextPiece} />
    </div>
  );
};
```

✅ When the game starts, a real random piece will appear in the preview.

💡 **AI Prompt:** "How can I test a React component that relies on Redux state?"

---

## 🧠 Stretch Challenges
- [ ] Add a label above the preview: "Next Block"
- [ ] Fade the piece in when it changes
- [ ] Use a queue to preview multiple upcoming blocks

---

## ➡️ Next Step
Next, we’ll connect the main board in [P12 – Connect Grid Board](../P12-Connect-Grid-Board) and begin rendering live game data!

