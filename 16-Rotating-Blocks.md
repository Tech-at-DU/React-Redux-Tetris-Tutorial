# 🔄 P16 – Rotating Blocks

Time to add the ability to **rotate tetrominoes**! In this step, you'll:
✅ Create a function to rotate a piece’s shape matrix  
✅ Add a Redux action to rotate the current piece  
✅ Trigger rotation with a keyboard input

---

## 1️⃣ Add Rotation Logic
In `src/features/game/gameUtils.js`, create a utility function:

```js
export function rotate(shape) {
  const size = shape.length;
  const newShape = Array.from({ length: size }, () => Array(size).fill(0));

  for (let row = 0; row < size; row++) {
    for (let col = 0; col < size; col++) {
      newShape[col][size - 1 - row] = shape[row][col];
    }
  }

  return newShape;
}
```

✅ This rotates a square matrix clockwise.

---

## 2️⃣ Add Action and Reducer
Open `gameSlice.js` and import the utility:

```js
import { rotate } from "./gameUtils";
```

Add a new reducer:

```js
rotatePiece(state) {
  if (state.currentPiece) {
    state.currentPiece.shape = rotate(state.currentPiece.shape);
  }
}
```

Add it to the exports:

```js
export const { startGame, resetGame, rotatePiece, ... } = gameSlice.actions;
```

✅ This updates the shape in Redux.

---

## 3️⃣ Trigger with Keyboard Input
In `TetrisGame.js`, listen for key presses:

```js
import { useEffect } from "react";
import { rotatePiece } from "../features/game/gameSlice";

useEffect(() => {
  const handleKeyDown = (e) => {
    if (e.code === "ArrowUp") {
      dispatch(rotatePiece());
    }
  };

  window.addEventListener("keydown", handleKeyDown);
  return () => window.removeEventListener("keydown", handleKeyDown);
}, [dispatch]);
```

✅ Pressing the ⬆️ arrow rotates the falling piece!

💡 **AI Prompt:** "How can I prevent invalid rotation that goes out of bounds in Tetris?"

---

## 🧠 Stretch Challenges
- [ ] Prevent rotation if it would overlap or exit the board
- [ ] Support different rotation states for non-square pieces
- [ ] Add animation when the piece rotates

---

## ➡️ Next Step
Now that your blocks can rotate, let’s start moving them left, right, and down in [P17 – Moving Blocks](../P17-Moving-Blocks)!

