# 🕹️ P13 – Connect Controls

It’s time to make your **Start** and **Reset** buttons functional! In this step, we’ll:
✅ Use Redux `dispatch` to trigger game actions  
✅ Connect the `Controls` component to the store  
✅ Wire the UI buttons to start and reset the game

---

## 1️⃣ Import Redux Actions
Open `TetrisGame.js` and update the top imports:

```js
import { useDispatch, useSelector } from "react-redux";
import { startGame, resetGame } from "../features/game/gameSlice";
```

---

## 2️⃣ Define Event Handlers
Still in `TetrisGame`, add these handlers:

```js
const dispatch = useDispatch();

const handleStart = () => {
  dispatch(startGame());
};

const handleReset = () => {
  dispatch(resetGame());
};
```

✅ These trigger Redux actions that update state when called.

---

## 3️⃣ Pass Handlers to `Controls`
In your return statement:

```jsx
<Controls onStart={handleStart} onReset={handleReset} />
```

✅ Buttons now trigger real game state updates!

💡 **AI Prompt:** “What happens inside the Redux store when I dispatch an action?”

---

## 4️⃣ Test it
- Click **Start Game** – the board should clear, and a new piece should spawn
- Click **Reset Game** – the game should return to its initial state

If you've connected `ScoreBoard` or `NextBlock`, those will also reset accordingly.

---

## 🧠 Stretch Challenges
- [ ] Disable **Start** button once game has started
- [ ] Replace **Reset** with **Pause/Resume** toggle
- [ ] Add keyboard bindings for Start (S) and Reset (R)

---

## ➡️ Next Step
In [P14 – Connect Message Popup](./14-Connect-Message-Popup.md), we’ll display overlays like "Game Over" using live state from Redux!

