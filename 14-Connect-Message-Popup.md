# 💬 P14 – Connect Message Popup

In this step, you’ll display message overlays like **“Game Over”**, **“Paused”**, or **“Get Ready!”** by connecting the `MessagePopup` component to Redux.

You’ll:
✅ Use Redux state to control when and what message is shown  
✅ Display the popup conditionally  
✅ Lay the groundwork for other game messages

---

## 1️⃣ Connect Game State in `TetrisGame`
In `TetrisGame.js`, import and use selectors:

```js
import MessagePopup from "./MessagePopup";

const isRunning = useSelector((state) => state.game.isRunning);
const gameOver = useSelector((state) => state.game.gameOver);
```

Then define a simple `message` variable:

```js
let message = "";
let showPopup = false;

if (gameOver) {
  message = "Game Over";
  showPopup = true;
} else if (!isRunning) {
  message = "Paused";
  showPopup = true;
}
```

---

## 2️⃣ Render the MessagePopup
Just above your return statement in `TetrisGame`:

```jsx
<MessagePopup message={message} isVisible={showPopup} />
```

✅ Now the popup appears automatically based on the game state.

💡 **AI Prompt:** “How can I handle conditional overlays in React cleanly with Redux?”

---

## 3️⃣ Add Game Over Test Option (Optional)
To test the Game Over overlay manually, dispatch `endGame()` from a debug button:

```js
import { endGame } from "../features/game/gameSlice";

<button onClick={() => dispatch(endGame())}>Trigger Game Over</button>
```

✅ This helps preview the overlay without full game logic yet.

---

## 🧠 Stretch Challenges
- [ ] Add a "Play Again" button inside the popup
- [ ] Use animation (fade, zoom) when popup appears
- [ ] Make `MessagePopup` reusable for other game states

---

## ➡️ Next Step
In [P15 – Connect Score Board](./15-Connect-Score-Board.md), we’ll wire up the live score, level, and lines cleared from Redux!

