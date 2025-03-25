## 🔄 P16 – Rotating Blocks

Time to make your tetrominoes rotate! We’ll add helper functions to determine valid rotations and update the Redux reducer to perform the rotation.

---

### 🎯 Goal

- Create utility functions for shape rotation and collision checking
- Handle the `rotate` action in the reducer

---

### 🧩 Step 1: Create Utility Functions

In `src/utils/index.js`, add these functions:

```js
// Return the next rotation index for a shape
export const nextRotation = (shape, rotation) => {
  return (rotation + 1) % shapes[shape].length;
};

// Check if a shape can move to x, y with a given rotation
export const canMoveTo = (shape, grid, x, y, rotation) => {
  const currentShape = shapes[shape][rotation];

  for (let row = 0; row < currentShape.length; row++) {
    for (let col = 0; col < currentShape[row].length; col++) {
      if (currentShape[row][col] !== 0) {
        const proposedX = col + x;
        const proposedY = row + y;

        if (proposedY < 0) continue;

        const possibleRow = grid[proposedY];

        if (
          !possibleRow ||
          possibleRow[proposedX] === undefined ||
          possibleRow[proposedX] !== 0
        ) {
          return false;
        }
      }
    }
  }

  return true;
};
```

✅ These helpers check if a rotation is valid based on the current grid and block position.

---

### 🧩 Step 2: Import Utilities in the Reducer

In `src/features/gameSlice.js`, import:

```js
import { defaultState, nextRotation, canMoveTo } from '../utils';
```

---

### 🧩 Step 3: Update the `rotate` Reducer

Find the existing placeholder:

```js
rotate: () => {},
```

Replace it with:

```js
rotate: (state) => {
  const { shape, grid, x, y, rotation } = state;
  const newRotation = nextRotation(shape, rotation);

  if (canMoveTo(shape, grid, x, y, newRotation)) {
    state.rotation = newRotation;
  }

  return state;
},
```

✅ This tries the next rotation and only applies it if the new position is valid.

---

### 🧪 Test It

Try setting the default state to display the block mid-board:

In `defaultState()` (in `utils.js`):

```js
y: 6,
rotation: 0,
shape: 3,
```

Then click the **Rotate** button — it should visually rotate through all the block’s shapes!

---

### 💬 Try This

- Manually cycle through `rotation` values and use `console.table(shapes[shape][rotation])` to see each version.
- Change `shape` in state to test other pieces.

---

### 🤖 AI Prompts

> "Why is rotation handled modulo the number of available shapes?"

> "How could you support counter-clockwise rotation?"

> "What does `canMoveTo()` return false for?"

---

### 🧠 Check for Understanding

- Why do we check `canMoveTo()` before updating `rotation`?
- Why is the shape index tied to both its color and its structure?
- What happens if we rotate a shape at the far left or right of the board?

---

### ✅ Commit Your Work

```bash
git add .
git commit -m "rotate reducer"
git push
```
