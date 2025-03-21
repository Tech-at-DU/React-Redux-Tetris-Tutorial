# 🧮 P15 – Connect Score Board

Time to hook up your `ScoreBoard` to real game data from Redux! In this step, you'll:
✅ Use `useSelector` to read the score, level, and lines cleared  
✅ Display live stats that update as the game progresses

---

## 1️⃣ Update `TetrisGame` to Pull Redux State
In `TetrisGame.js`, use selectors to get game stats:

```js
const score = useSelector((state) => state.game.score);
const level = useSelector((state) => state.game.level);
const linesCleared = useSelector((state) => state.game.linesCleared);
```

Then pass them into the `ScoreBoard`:

```jsx
<ScoreBoard score={score} level={level} linesCleared={linesCleared} />
```

✅ Now your score panel reflects real-time game stats.

---

## 2️⃣ Test It Manually (Optional)
To preview live updates:

```js
import { useDispatch } from "react-redux";
import { startGame } from "../features/game/gameSlice";

// Dispatch fake data to test it:
const dispatch = useDispatch();
useEffect(() => {
  dispatch(startGame());
}, [dispatch]);
```

✅ You should see the score, level, and lines reset when the game starts.

💡 **AI Prompt:** "What’s a clean way to derive display data from Redux in React components?"

---

## 🧠 Stretch Challenges
- [ ] Add animation when score increases
- [ ] Display high score (track across sessions)
- [ ] Color-code level or use icons to enhance feedback

---

## ➡️ Next Step
Now that the interface is fully wired up, we’re ready to begin **actual gameplay mechanics** like movement and collision in [P16 – Rotating Blocks](../P16-Rotating-Blocks)!
