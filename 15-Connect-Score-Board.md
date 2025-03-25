## 🧮 P15 – Connect ScoreBoard

Time to connect the ScoreBoard to the Redux store — including the **score**, **play/pause**, and **restart** logic.

---

### 🎯 Goal

- Display the current score from state
- Show a dynamic "Play/Pause" button
- Add a working "Restart" button

---

### 🧩 Step 1: Import Redux Tools and Actions

Open `src/components/ScoreBoard.js` and at the top add:

```js
import { useSelector, useDispatch } from 'react-redux';
import { pause, resume, restart } from '../features/gameSlice';
```

✅ This gives you everything you need to connect and dispatch.

---

### 🧩 Step 2: Read State & Set Up Dispatch

Inside your component:

```js
export default function ScoreBoard() {
  const dispatch = useDispatch();
  const { score, isRunning, gameOver } = useSelector((state) => state);
  // ...
```

---

### 🧩 Step 3: Display Score

Update the score display line:

```jsx
<div>Score: {score}</div>
```

✅ This now shows the real score from Redux.

---

### 🧩 Step 4: Handle Restart

Update the Restart button:

```jsx
<button
  className="score-board-button"
  onClick={() => dispatch(restart())}
>
  Restart
</button>
```

---

### 🧩 Step 5: Handle Play/Pause Logic

Replace the Play button with:

```jsx
<button
  className="score-board-button"
  onClick={() => {
    if (gameOver) return;
    if (isRunning) {
      dispatch(pause());
    } else {
      dispatch(resume());
    }
  }}
>
  {isRunning ? 'Pause' : 'Play'}
</button>
```

✅ This button now toggles based on the current game state.

### Challenge! 

Create a subcomponent for each of these buttons. 

solving this challenge will illustrate the advantages of using Redux to manage state! 

---

### 🧪 Test Ideas

You can test by mocking the default state in `utils.js`:

```js
score: 23000,
isRunning: true,
gameOver: false
```

You should see:

- Score: 23000
- Button shows “Pause”
- Buttons are clickable

Try also:

- `gameOver: true` → "Play" button does nothing
- `isRunning: false` → Button shows "Play"

---

### 💬 Try This

- Replace the button labels with icons or emojis
- Add a level display next to the score

---

### 🤖 AI Prompts

> "How could the score increase automatically based on game events?"

> "Why is `dispatch(pause())` not called directly inside a ternary expression?"

> "How could we unit test this component with mock state?"

---

### 🧠 Check for Understanding

- Why do we check `gameOver` before dispatching?
- How does this component avoid prop-drilling?
- Why is `useDispatch` needed here?

---

### ✅ Commit Your Work

```bash
git add .
git commit -m "Added connection for score board"
git push
```
