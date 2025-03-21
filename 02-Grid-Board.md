# 🧱 P02 – Grid Board

Now that you have individual `GridSquare` components, it’s time to build a **grid-based board** that displays the entire Tetris play area.

In this step, you’ll:
✅ Create a 2D grid layout using `GridSquare`
✅ Generate grid squares dynamically from a JavaScript array
✅ Prepare for connecting the board to game state

---

## 🧩 Step 1: Create the GridBoard Component
Create a file: `src/components/GridBoard.js`

```jsx
import React from "react";
import GridSquare from "./GridSquare";
import "./GridBoard.css";

const GridBoard = ({ board }) => {
  const width = board[0].length;
  const flatBoard = board.flat();

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

📌 This component flattens the 2D board array and renders a `GridSquare` for each cell.

💡 **AI Prompt:**
*“How do you convert a 2D array into a 1D array in JavaScript?”*

---

## 🎨 Step 2: Add GridBoard Styling
Create `src/components/GridBoard.css`

```css
.grid-board {
  display: grid;
  background: #111;
  border: 2px solid #444;
}
```

✅ The number of columns adjusts dynamically based on board width.

---

## 🧪 Step 3: Preview It with Test Data
In `App.js`, try rendering the board with mock data:

```jsx
import React from "react";
import GridBoard from "./components/GridBoard";

const testBoard = Array(20)
  .fill(null)
  .map(() => Array(10).fill({ color: "#ccc" }));

function App() {
  return (
    <div>
      <h1>Tetris Grid Test</h1>
      <GridBoard board={testBoard} />
    </div>
  );
}

export default App;
```

✅ **Checkpoint:** You should see a 10x20 grid filled with gray squares.

---

## 🧠 Stretch Challenges
- [ ] Add props for grid size (height and width)
- [ ] Alternate colors every other row for debugging
- [ ] Add a frame or drop-shadow around the board

---

## ➡️ Next Step
In [P03 – Next Block](../P03-Next-Block), we’ll create a separate mini-board to preview the upcoming piece!
