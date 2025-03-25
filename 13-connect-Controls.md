## 🕹️ P13 – Connect Controls

Let’s make the control buttons **dispatch Redux actions** to move and rotate the falling blocks.

---

### 🎯 Goal

- Use `useDispatch` to trigger movement and rotation actions
- Use `useSelector` to read `isRunning` and disable buttons when paused

---

### 🧩 Step 1: Set Up Redux in Controls

Edit `src/components/Controls.js` and import:

```js
import React from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { moveDown, moveLeft, moveRight, rotate } from '../features/gameSlice';
```

Inside the component, initialize Redux:

```js
const dispatch = useDispatch();
const { isRunning } = useSelector((state) => state);
```

✅ This gives us the dispatch function and access to the current game state.

---

### 🧩 Step 2: Connect the Buttons

Update the return block of `Controls` with the following:

```jsx
<div className="controls">
  {/* Left */}
  <button
    disabled={!isRunning}
    className="control-button"
    onClick={() => dispatch(moveLeft())}
  >
    Left
  </button>

  {/* Right */}
  <button
    disabled={!isRunning}
    className="control-button"
    onClick={() => dispatch(moveRight())}
  >
    Right
  </button>

  {/* Rotate */}
  <button
    disabled={!isRunning}
    className="control-button"
    onClick={() => dispatch(rotate())}
  >
    Rotate
  </button>

  {/* Down */}
  <button
    disabled={!isRunning}
    className="control-button"
    onClick={() => dispatch(moveDown())}
  >
    Down
  </button>
</div>
```

✅ Each button now issues an action when clicked — only if the game is running.

You won't see the effect of pressing these buttons yet, since the game is not yet running!

---

### 💬 Try This

- Set `isRunning: false` in `defaultState()` in `utils.js` to test disabled buttons.
- Add a `console.log("Move Left")` inside `onClick` to verify dispatching.

---

### 🤖 AI Prompts

> "What does the `dispatch()` function actually do in Redux?"

> "What is the purpose of `useSelector` and how does it optimize re-renders?"

> "How could you handle key presses instead of buttons?"

---

### 🧠 Check for Understanding

- What does the `disabled={!isRunning}` check do?
- Why is `moveLeft()` a function instead of just a variable?
- What would happen if you forgot to `import` the action?

---

### ✅ Commit Your Work

```bash
git add .
git commit -m "Added connection for controls"
git push
```
