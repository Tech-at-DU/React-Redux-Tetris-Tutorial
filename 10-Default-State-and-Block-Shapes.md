# 🧩 P10 – Default State & Block Shapes

With your Redux slice and folder structure in place, let’s define the default **Tetris board**, **block shapes**, and helper functions to manage them. This is the foundation for rendering real game pieces.

You’ll:
✅ Create reusable block definitions  
✅ Initialize a default game board  
✅ Lay groundwork for rendering moving pieces

---

## 1️⃣ Define Block Shapes
Create a file: `src/features/game/pieceShapes.js`

```js
export const SHAPES = {
  I: [
    [0, 0, 0, 0],
    [1, 1, 1, 1],
    [0, 0, 0, 0],
    [0, 0, 0, 0],
  ],
  O: [
    [1, 1],
    [1, 1],
  ],
  T: [
    [0, 1, 0],
    [1, 1, 1],
    [0, 0, 0],
  ],
  L: [
    [0, 0, 1],
    [1, 1, 1],
    [0, 0, 0],
  ],
  J: [
    [1, 0, 0],
    [1, 1, 1],
    [0, 0, 0],
  ],
  S: [
    [0, 1, 1],
    [1, 1, 0],
    [0, 0, 0],
  ],
  Z: [
    [1, 1, 0],
    [0, 1, 1],
    [0, 0, 0],
  ],
};

export const COLORS = {
  0: "#000", // empty
  1: "#0ff", // I
  2: "#ff0", // O
  3: "#f0f", // T
  4: "#f90", // L
  5: "#00f", // J
  6: "#0f0", // S
  7: "#f00", // Z
};
```

📌 `SHAPES` defines the geometry of each piece, and `COLORS` maps block types to colors.

---

## 2️⃣ Create Board Helpers
Create `src/features/game/gameUtils.js`

```js
export const createEmptyBoard = (rows = 20, cols = 10) => {
  return Array.from({ length: rows }, () =>
    Array.from({ length: cols }, () => ({ color: "#000" }))
  );
};
```

✅ This creates a clean 20x10 grid filled with black squares.

---

## 3️⃣ Generate a Random Block
Add this to `gameUtils.js`:

```js
import { SHAPES, COLORS } from "./pieceShapes";

export const generateRandomPiece = () => {
  const keys = Object.keys(SHAPES);
  const randomKey = keys[Math.floor(Math.random() * keys.length)];
  const shape = SHAPES[randomKey];
  const color = COLORS[keys.indexOf(randomKey) + 1];

  return {
    shape,
    color,
    position: { row: 0, col: 3 },
  };
};
```

📌 This will be used to spawn blocks on game start and after lines clear.

💡 **AI Prompt:** "What’s the best way to store game pieces and their properties in Redux?"

---

## ✅ Checkpoint
You now have a full system for:
- Creating a fresh board
- Defining and styling Tetris pieces
- Randomly generating a piece with shape, color, and position

---

## 🧠 Stretch Challenges
- [ ] Add rotation states for each shape
- [ ] Preload more than one next piece
- [ ] Use TypeScript or JSDoc to define piece types

---

## ➡️ Next Step
In [P11 – Connect Next Block](../P11-Connect-Next-Block), you’ll connect your preview UI to show real random pieces!

