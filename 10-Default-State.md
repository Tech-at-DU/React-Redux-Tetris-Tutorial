## 🧩 P10 – State & Shapes

Let’s build out the core logic for representing the game board and tetromino shapes in Redux state.

---

### 🎯 Goal

- Define the game’s default state
- Build shape arrays (with all rotations)
- Write helper functions for shapes, board setup, and randomness

---

### 🧩 Step 1: Create a Default Grid

In `src/utils/index.js`, add:

```js
export const gridDefault = () => {
  const rows = 18;
  const cols = 10;
  const array = [];
  for (let row = 0; row < rows; row++) {
    array.push([]);
    for (let col = 0; col < cols; col++) {
      array[row].push(0);
    }
  }
  return array;
};
```

✅ This generates an 18×10 grid filled with `0`s.

---

### 🧩 Step 2: Define All Tetromino Shapes

Also in `src/utils/index.js`, add the full shape structure (you already have this in your doc):

```js
export const shapes = [
  // none
  [
    [
      [0,0,0,0],
      [0,0,0,0],
      [0,0,0,0],
      [0,0,0,0]]],

  // I
  [
    [
      [0,0,0,0],
      [1,1,1,1],
      [0,0,0,0],
      [0,0,0,0]],

    [
      [0,1,0,0],
      [0,1,0,0],
      [0,1,0,0],
      [0,1,0,0]]],

  // T
  [
    [
      [0,0,0,0],
    [1,1,1,0],
    [0,1,0,0],
    [0,0,0,0]],

    [
      [0,1,0,0],
      [1,1,0,0],
      [0,1,0,0],
      [0,0,0,0]],

    [
      [0,1,0,0],
      [1,1,1,0],
      [0,0,0,0],
      [0,0,0,0]],

    [
      [0,1,0,0],
      [0,1,1,0],
      [0,1,0,0],
      [0,0,0,0]]],

  // L
  [
    [
      [0,0,0,0],
      [1,1,1,0],
      [1,0,0,0],
      [0,0,0,0]],

    [
      [1,1,0,0],
      [0,1,0,0],
      [0,1,0,0],
      [0,0,0,0]],

    [
      [0,0,1,0],
      [1,1,1,0],
      [0,0,0,0],
      [0,0,0,0]],

    [
      [0,1,0,0],
      [0,1,0,0],
      [0,1,1,0],
      [0,0,0,0]]],

  // J
  [
    [
      [1,0,0,0],
      [1,1,1,0],
      [0,0,0,0],
      [0,0,0,0]],

    [
      [0,1,1,0],
      [0,1,0,0],
      [0,1,0,0],
      [0,0,0,0]],

    [
      [0,0,0,0],
      [1,1,1,0],
      [0,0,1,0],
      [0,0,0,0]],

    [
      [0,1,0,0],
      [0,1,0,0],
      [1,1,0,0],
      [0,0,0,0]]],

  // Z
  [
    [
      [0,0,0,0],
      [1,1,0,0],
      [0,1,1,0],
      [0,0,0,0]],

    [
      [0,0,1,0],
      [0,1,1,0],
      [0,1,0,0],
      [0,0,0,0]]],

  // S
  [
    [
      [0,0,0,0],
      [0,1,1,0],
      [1,1,0,0],
      [0,0,0,0]],

    [
      [0,1,0,0],
      [0,1,1,0],
      [0,0,1,0],
      [0,0,0,0]]],

  // O
  [
    [
      [0,1,1,0],
      [0,1,1,0],
      [0,0,0,0],
      [0,0,0,0]]]
];
```

✅ Each shape is a 4×4 grid, grouped by rotation. The shape index matches its color.

IF the block of code above isn't making sense try this AI prompt: 

> "<paste the code block above here> This somehow describes the blocks in the game Tetris, how does that work?"

---

### 🧩 Step 3: Add Utility Functions

Add these to `src/utils/index.js`:

```js
// Pick a random shape index (skip index 0)
export const randomShape = () => {
  return random(1, shapes.length - 1);
};
```

✅ This keeps your random generation centralized and reusable.

---

### 🧩 Step 4: Create the Default Game State

Still in `src/utils/index.js`, add:

```js
export const defaultState = () => {
  return {
    grid: gridDefault(),
    shape: randomShape(),
    rotation: 0,
    x: 5,
    y: -4,
    nextShape: randomShape(),
    isRunning: true,
    score: 0,
    speed: 1000,
    gameOver: false
  };
};
```

✅ This provides the initial Redux state with shape position, board, and game logic.

---

### 🧩 Step 5: Connect to Redux Slice

Edit `src/features/gameSlice.js`:

```js
import { createSlice } from '@reduxjs/toolkit';
import { defaultState } from '../utils';

export const gameSlice = createSlice({
  name: 'game',
  initialState: defaultState(),
  reducers: {
    pause: () => {},
    resume: () => {},
    moveLeft: () => {},
    moveRight: () => {},
    moveDown: () => {},
    rotate: () => {},
    gameOver: () => {},
    restart: () => {}
  },
});

export const {
  pause, resume, moveLeft, moveRight,
  moveDown, rotate, gameOver, restart
} = gameSlice.actions;

export default gameSlice.reducer;
```

✅ Now the app starts with a complete, randomized default game state.

---

### 💬 Try This

- Log the default state in `App.js` using `useSelector()` to view the state shape.
- Use `console.table(gridDefault())` in the browser console to visualize the board.

---

### 🤖 AI Prompts

> "'m working on the game Tetris using Redux Toolkit. This is my gameSlice explain this to me as a beginner, intermediate, and advanced. <paste the code from gameSlice.js here>"

> "How could you animate a tetromino falling based on this state?"

> "What are some alternatives to using arrays to model a game grid?"

> "Why is `y: -4` used as the starting vertical position?"

---

### 🧠 Check for Understanding

- How does the shape index relate to color and rotation?
- What’s the benefit of storing shapes as arrays instead of components?
- How is this state structured to support rotation and collision logic?

---

### ✅ Commit Your Work

```bash
git add .
git commit -m "Added state utils"
git push
```
