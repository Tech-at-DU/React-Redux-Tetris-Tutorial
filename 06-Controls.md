# 🎮 P06 – Controls

Now let’s give the player some control over the game! In this step, you’ll:
✅ Add Start and Reset buttons  
✅ Create a `Controls` component  
✅ Style the controls for consistency with the layout

Later, we’ll wire these up to Redux to start and reset the game.

---

## 🧩 Step 1: Create the Controls Component
Create a file: `src/components/Controls.js`

```jsx
import React from "react";
import "./Controls.css";

const Controls = ({ onStart, onReset }) => {
  return (
    <div className="controls">
      <button onClick={onStart}>Start Game</button>
      <button onClick={onReset}>Reset Game</button>
    </div>
  );
};

export default Controls;
```

---

## 🎨 Step 2: Add Control Styles
Create a file: `src/components/Controls.css`

```css
.controls {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.controls button {
  font-size: 16px;
  padding: 10px 16px;
  border: none;
  border-radius: 4px;
  background-color: #3498db;
  color: white;
  cursor: pointer;
  transition: background 0.2s ease;
}

.controls button:hover {
  background-color: #2980b9;
}
```

✅ Buttons are stacked vertically and styled to match the rest of the UI.

---

## 🧪 Step 3: Add Controls to `TetrisGame`
Update `TetrisGame.js`:

```jsx
import Controls from "./Controls";

const handleStart = () => alert("Start pressed!");
const handleReset = () => alert("Reset pressed!");

<Controls onStart={handleStart} onReset={handleReset} />
```

Place it inside the `.tetris-right` column below `ScoreBoard`.

✅ **Checkpoint:** Buttons should appear styled and stacked, and show alerts when clicked.

---

## 🧠 Stretch Challenges
- [ ] Add keyboard shortcuts (e.g., S to start, R to reset)
- [ ] Disable Start button while game is running
- [ ] Add an option to pause/resume

---

## ➡️ Next Step
In [P07 – Message Popup](../P07-Message-Popup), you’ll build a modal to display messages like "Game Over" and "Paused"!

