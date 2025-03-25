## 🧊 P17 – Moving Blocks

Now that we can rotate, let’s add movement: **left**, **right**, and **down** — with grid placement and scoring logic!

---

### 🎯 Goal

- Handle `moveLeft` and `moveRight` in the reducer
- Write utility functions for placing blocks and scoring
- Handle `moveDown` with full logic: placement, new block, scoring, game over

---

## 🧩 Step 1: moveLeft Reducer

In `src/features/gameSlice.js`:

```js
moveLeft: (state) => {
  const { shape, grid, x, y, rotation } = state;
  if (canMoveTo(shape, grid, x - 1, y, rotation)) {
    state.x = x - 1;
  }
  return state;
},
```

✅ This moves the block left if there's room.

---

### 🧩 Step 2: moveRight Reducer

```js
moveRight: (state) => {
  const { shape, grid, x, y, rotation } = state;
  if (canMoveTo(shape, grid, x + 1, y, rotation)) {
    state.x = x + 1;
  }
  return state;
},
```

✅ This mirrors `moveLeft`, but shifts right.

---

## 🧩 Step 3: Utility – `addBlockToGrid`

In `src/utils/index.js`:

```js
export const addBlockToGrid = (shape, grid, x, y, rotation) => {
  const block = shapes[shape][rotation];
  const newGrid = [...grid];

  for (let row = 0; row < block.length; row++) {
    for (let col = 0; col < block[row].length; col++) {
      if (block[row][col]) {
        newGrid[row + y][col + x] = shape;
      }
    }
  }

  return newGrid;
};
```

✅ Places a shape onto a copy of the current grid.

---

### 🧩 Step 4: Utility – `checkRows`

```js
export const checkRows = (grid) => {
  const points = [0, 40, 100, 300, 1200];
  let completedRows = 0;

  for (let row = 0; row < grid.length; row++) {
    if (grid[row].indexOf(0) === -1) {
      completedRows++;
      grid.splice(row, 1);
      grid.unshift(Array(10).fill(0));
    }
  }

  return points[completedRows];
};
```

✅ Detects and scores cleared rows, adjusts grid.

---

## 🧩 Step 5: moveDown Reducer

Make sure this is imported at the top of `gameSlice.js`:

```js
import {
  defaultState,
  nextRotation,
  canMoveTo,
  addBlockToGrid,
  checkRows,
  randomShape,
} from '../utils';
```

Then update the reducer:

```js
moveDown: (state) => {
  const { x, y, shape, grid, rotation, nextShape } = state;
  const maybeY = y + 1;

  if (canMoveTo(shape, grid, x, maybeY, rotation)) {
    state.y = maybeY;
    return state;
  }

  // Can't move down: lock block into grid
  const newGrid = addBlockToGrid(shape, grid, x, y, rotation);

  state.grid = newGrid;
  state.x = 3;
  state.y = -4;
  state.rotation = 0;
  state.shape = nextShape;
  state.nextShape = randomShape();

  // Game over check
  if (!canMoveTo(state.shape, newGrid, state.x, state.y, state.rotation)) {
    state.shape = 0;
    state.gameOver = true;
    return state;
  }

  state.score += checkRows(newGrid);
  return state;
},
```

✅ This reducer:
- Moves down if it can
- Otherwise places the block
- Spawns the next shape
- Checks for game over
- Scores completed rows

---

### 💬 Try This

- Click the Down button a few times. A block should appear, and move down the screen. Remember, the block starts at y of -4. 
- After the block is visible try clicking left and right. The block should move left and right. 
- Move the block all the way to the left, it should stop at when it hits the left side of the grid. Try the right side. 
- Press down until the block hits the botton of the grid. The block should stop. This should create a new block at y of -4. 
- Move the new block down until it hits the previous block. It should stop when it hist the existing block. 
- Fill a row with blocks. When a row is completely filled it should disappear, move the colored squares above it down, and update the score. 

**Pro tip:** When testing your work, think of what you have down and how you can perform a test of that software system. 

When testing, think of all of the possible things your software should able to do, and test each of these things. 

Be methodical! Test each feature, think of what the limits and edge cases are, and test each of those. Think about is happening, especially of things are not working! Of what you expect to happen, and what you are observing! 

---

### 🤖 AI Prompts

> "How does the reducer avoid modifying the original grid?"

> "Why do we use `randomShape()` and `checkRows()` after locking a piece?"

> "What logic prevents spawning a new shape during game over?"

---

### 🧠 Check for Understanding

- Why does `moveDown` include so many responsibilities?
- What happens if a shape starts in an invalid spot?
- How does `splice()` + `unshift()` simulate gravity in the grid?

---

### ✅ Commit Your Work

```bash
git add .
git commit -m "move left and right"
git push
```
