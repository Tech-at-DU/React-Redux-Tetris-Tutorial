# 🔮 P03 – Next Block

In Tetris, it’s helpful to see which block is coming next. In this step, you’ll build a **mini board** to preview the next block using the same `GridSquare` component.

You’ll:
✅ Reuse `GridBoard` to display the next piece  
✅ Normalize the block data to fit a 4x4 preview area  
✅ Prepare for integration with game state later

---

## 🔁 Step 1: Create the NextBlock Component
Create a new file: `src/components/NextBlock.js`

```jsx
import React from "react";
import GridSquare from "./GridSquare";
import "./GridBoard.css";

const NextBlock = ({ shape }) => {
  const block = shape.flat();

  return (
    <div
      className="grid-board"
      style={{
        width: "120px",
        gridTemplateColumns: `repeat(4, 1fr)`
      }}
    >
      {block.map((cell, i) => (
        <GridSquare key={i} color={cell.color} />
      ))}
    </div>
  );
};

export default NextBlock;
```

📌 This component accepts a `shape` prop (a 4x4 matrix) and displays it in a fixed-size grid.

💡 **AI Prompt:**
"What are some ways to visualize 2D data in React?"

---

## 🧪 Step 2: Test With a Sample Shape
In `App.js`, test the component with sample shape data:

```jsx
import React from "react";
import NextBlock from "./components/NextBlock";

const testShape = [
  [ { color: "#000" }, { color: "#000" }, { color: "#000" }, { color: "#000" } ],
  [ { color: "#0ff" }, { color: "#0ff" }, { color: "#0ff" }, { color: "#0ff" } ],
  [ { color: "#000" }, { color: "#000" }, { color: "#000" }, { color: "#000" } ],
  [ { color: "#000" }, { color: "#000" }, { color: "#000" }, { color: "#000" } ]
];

function App() {
  return (
    <div>
      <h1>Next Block Test</h1>
      <NextBlock shape={testShape} />
    </div>
  );
}

export default App;
```

✅ You should see a cyan horizontal line in the center.

---

## 🧠 Stretch Challenges
- [ ] Add a label above the preview: “Next Block”
- [ ] Adjust preview alignment to center shapes better
- [ ] Animate the block when it changes

---

## ➡️ Next Step
Now that the preview is in place, we’ll build the UI for tracking score and level in [P04 – Score Board](./04-Score-Board.md)!

