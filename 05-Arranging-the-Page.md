# 📐 P05 – Arranging the Page

Now that you’ve built the UI components for the game grid, next block, and score display, it’s time to **arrange them together into a full game layout**.

You’ll:
✅ Create a responsive page layout using CSS Flexbox  
✅ Combine `GridBoard`, `NextBlock`, and `ScoreBoard`  
✅ Prepare the interface for control buttons in a future step

---

## 🧱 Step 1: Create a `TetrisGame` Component
Create a file: `src/components/TetrisGame.js`

```jsx
import React from "react";
import GridBoard from "./GridBoard";
import NextBlock from "./NextBlock";
import ScoreBoard from "./ScoreBoard";
import "./TetrisGame.css";

const testBoard = Array(20).fill(null).map(() => Array(10).fill({ color: "#ccc" }));
const testShape = [
  [ { color: "#000" }, { color: "#0ff" }, { color: "#0ff" }, { color: "#000"} ],
  [ { color: "#000" }, { color: "#0ff" }, { color: "#0ff" }, { color: "#000"} ],
  [ { color: "#000" }, { color: "#000" }, { color: "#000" }, { color: "#000"} ],
  [ { color: "#000" }, { color: "#000" }, { color: "#000" }, { color: "#000"} ]
];

const TetrisGame = () => {
  return (
    <div className="tetris-container">
      <div className="tetris-left">
        <GridBoard board={testBoard} />
      </div>
      <div className="tetris-right">
        <NextBlock shape={testShape} />
        <ScoreBoard score={500} level={2} linesCleared={5} />
      </div>
    </div>
  );
};

export default TetrisGame;
```

---

## 🎨 Step 2: Add Layout Styles
Create a file: `src/components/TetrisGame.css`

```css
.tetris-container {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  gap: 40px;
  padding: 20px;
}

.tetris-left {
  flex-shrink: 0;
}

.tetris-right {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 20px;
}
```

✅ This gives you a simple two-column layout with spacing between components.

---

## 🧪 Step 3: Use in `App.js`
Update `App.js`:

```jsx
import React from "react";
import TetrisGame from "./components/TetrisGame";

function App() {
  return (
    <div>
      <h1>React Tetris</h1>
      <TetrisGame />
    </div>
  );
}

export default App;
```

✅ **Checkpoint:** You should see your Tetris grid on the left, with next block and score on the right.

---

## 🧠 Stretch Challenges
- [ ] Add a fixed width container around the full game
- [ ] Include a header with game title and controls placeholder
- [ ] Make layout responsive for small screens (media queries)

---

## ➡️ Next Step
Now that our layout is in place, we’ll build the control buttons in [P06 – Controls](./06-Controls.md)!

