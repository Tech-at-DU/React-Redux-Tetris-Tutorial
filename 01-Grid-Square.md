# 🔳 P01 – Grid Square

In this step, you’ll create the **smallest visual building block** of the Tetris board: the **Grid Square**. Each square represents one unit on the board, and its color will indicate whether it’s part of a falling block, a settled piece, or empty space.

---

## 🎯 What You’ll Build
A simple React component that:
- Renders a square `div`
- Applies a background color from props
- Can be reused throughout the game board

---

## 🧱 Step 1: Create the Component
Create a file: `src/components/GridSquare.js`

```jsx
import React from "react";
import "./GridSquare.css";

const GridSquare = ({ color = "#ccc" }) => {
  return <div className="grid-square" style={{ backgroundColor: color }}></div>;
};

export default GridSquare;
```

📌 This component accepts a `color` prop and renders a single square.

💡 **AI Prompt:**
*“What’s the difference between inline styles and CSS classes in React?”*

---

## 🎨 Step 2: Add Styling
Create a new file: `src/components/GridSquare.css`

```css
.grid-square {
  width: 30px;
  height: 30px;
  border: 1px solid #999;
  box-sizing: border-box;
}
```

You can update these dimensions later to make the game board responsive.

---

## ✅ Checkpoint
You now have a reusable square component! Next, you’ll use it to build a full **Grid Board** in the next step.

---

## 🧠 Stretch Challenges
- [ ] Allow props for `size` in addition to color
- [ ] Add hover styles for debugging layout
- [ ] Use CSS variables for dynamic theming

---

## ➡️ Next Step
Move on to [P02 – Grid Board](./02-Grid-Board.md) to assemble the game board out of `GridSquare` components!

