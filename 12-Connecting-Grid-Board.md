## 🧩 P12 – Connect GridBoard

It’s time to render the **actual game board** from Redux state — including the **current falling block**.

---

### 🎯 Goal

- Use Redux to pull game data into `GridBoard`
- Overlay the current block onto the grid using shape, rotation, x, and y
- Display each square with its correct color

---

### 🧩 Step 1: Set Up the Component

Update `src/components/GridBoard.js`:

```js
import React from 'react';
import { useSelector } from 'react-redux';
import GridSquare from './GridSquare';
import { shapes } from '../utils';
```

Then in your component:

```js
export default function GridBoard() {
  const { grid, shape, rotation, x, y } = useSelector((state) => state);

  const block = shapes[shape][rotation];
  const blockColor = shape;
  // ...
```

---

### 🧩 Step 2: Render the Grid + Block

Replace your existing mapping logic with this:

```js
  const gridSquares = grid.map((rowArray, row) =>
    rowArray.map((square, col) => {
      const blockX = col - x;
      const blockY = row - y;
      let color = square;

      if (
        blockX >= 0 && blockX < block.length &&
        blockY >= 0 && blockY < block.length
      ) {
        if (block[blockY][blockX]) {
          color = blockColor;
        }
      }

      const k = row * grid[0].length + col;
      return <GridSquare key={k} color={color} />;
    })
  );
```

✅ This maps the **4x4 block** onto the board at position `(x, y)`.

---

### 🧩 Step 3: Return the Board

Wrap it up:

```js
  return <div className="grid-board">{gridSquares}</div>;
}
```

✅ Your game board now reflects real state, and the current falling piece is mapped correctly — even if it starts off-screen.

---

### 🧪 Debug Tips

> Not seeing the falling block?

The shape starts at `y = -4`, so it’s **off the top**. Temporarily change:

```js
const blockY = row - y;
```

to:

```js
const blockY = row - 10;
```

Or in `defaultState()`, set `y: 10` to test.

---

### 💬 Try This

- Refresh the game — do you see different shapes appear at different times?
- Try logging `grid`, `x`, and `y` in the component to understand what’s being rendered.

---

### 🤖 AI Prompts

> "How does the current shape’s position get mapped into the game grid?"

> "Could you extract the block mapping logic into a reusable function?"

> "How would you detect collisions between the shape and existing blocks?"

---

### 🧠 Check for Understanding

- Why do we subtract `x` and `y` from `col` and `row`?
- How does this mapping logic handle rotation?
- Why does the grid array represent both empty space and static blocks?

---

### ✅ Commit Your Work

```bash
git add .
git commit -m "Added connection for grid board"
git push
```
