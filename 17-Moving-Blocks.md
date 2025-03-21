# ⬅️➡️⬇️ P17 – Moving Blocks

Now that pieces can rotate, let’s move them left, right, and down! In this step, you’ll:
✅ Add Redux actions to move pieces  
✅ Update the reducer to shift position  
✅ Trigger moves with keyboard input

---

## 1️⃣ Add Move Actions to Reducer
In `gameSlice.js`, add these reducers:

```js
moveLeft(state) {
  if (state.currentPiece) {
    state.currentPiece.position.col -= 1;
  }
},
moveRight(state) {
  if (state.currentPiece) {
    state.currentPiece.position.col += 1;
  }
},
moveDown(state) {
  if (state.currentPiece) {
    state.currentPiece.position.row += 1;
  }
},
```

✅ These update the current piece’s column and row.

Also export them:

```js
export const { moveLeft, moveRight, moveDown, ... } = gameSlice.actions;
```

---

## 2️⃣ Add Key Controls in `TetrisGame`
Update the `handleKeyDown` function:

```js
import { moveLeft, moveRight, moveDown } from "../features/game/gameSlice";

const handleKeyDown = (e) => {
  switch (e.code) {
    case "ArrowLeft":
      dispatch(moveLeft());
      break;
    case "ArrowRight":
      dispatch(moveRight());
      break;
    case "ArrowDown":
      dispatch(moveDown());
      break;
    case "ArrowUp":
      dispatch(rotatePiece());
      break;
    default:
      break;
  }
};
```

✅ Now you can move pieces with ⬅️ ➡️ ⬇️!

💡 **AI Prompt:** “How do I prevent a piece from moving through other blocks or off the grid?”

---

## 🧪 Step 3: Test Movement
- Start the game
- Use ⬅️ and ➡️ to move the piece sideways
- Use ⬇️ to drop it faster

✅ The game board should reflect your moves in real time.

---

## 🧠 Stretch Challenges
- [ ] Add collision detection to stop illegal moves
- [ ] Accelerate piece while holding ⬇️
- [ ] Snap piece down with spacebar (hard drop)

---

## ➡️ Next Step
Now that pieces move, let’s update the timer and automate piece drops in [P18 – Creating a Timer](../P18-Creating-a-Timer)!

