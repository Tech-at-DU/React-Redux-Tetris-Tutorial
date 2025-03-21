# 🧮 P04 – Score Board

Now that the main game grid and next block preview are working, let’s build the **Score Board** UI. This component will display the player’s **current score**, **level**, and **number of cleared lines**.

You’ll:
✅ Create a presentational component to show stats  
✅ Add styling for alignment and emphasis  
✅ Prepare to connect it to Redux state later

---

## 1️⃣ Create the ScoreBoard Component
Create a file: `src/components/ScoreBoard.js`

```jsx
import React from "react";
import "./ScoreBoard.css";

const ScoreBoard = ({ score, level, linesCleared }) => {
  return (
    <div className="score-board">
      <div><strong>Score:</strong> {score}</div>
      <div><strong>Level:</strong> {level}</div>
      <div><strong>Lines:</strong> {linesCleared}</div>
    </div>
  );
};

export default ScoreBoard;
```

💡 This component receives data via props. Later, we’ll connect it to Redux using `useSelector`.

---

## 2️⃣ Add Styles
Create a file: `src/components/ScoreBoard.css`

```css
.score-board {
  padding: 10px;
  background-color: #222;
  color: #fff;
  border-radius: 6px;
  margin-top: 10px;
  text-align: left;
}
.score-board div {
  margin: 5px 0;
  font-size: 18px;
}
```

✅ The board is styled to be visually distinct and readable.

---

## 3️⃣ Test the Component
Update your `App.js` to test the score board:

```jsx
import React from "react";
import ScoreBoard from "./components/ScoreBoard";

function App() {
  return (
    <div>
      <h1>ScoreBoard Test</h1>
      <ScoreBoard score={1200} level={3} linesCleared={14} />
    </div>
  );
}

export default App;
```

✅ **Checkpoint:** The component displays score, level, and lines clearly with dark background styling.

---

## 🧠 Stretch Challenges
- [ ] Add animation when score increases
- [ ] Display high score alongside current score
- [ ] Let the component format numbers with commas or spaces

---

## ➡️ Next Step
With all the core UI in place, we’ll begin assembling the page layout in [P05 – Arranging the Page](./05-Arranging-the-Page.md)!

