## ⏱️ P18 – Creating a Timer

Let’s make the game feel *real* — blocks will now fall automatically using `requestAnimationFrame`.

---

### 🎯 Goal

- Use `requestAnimationFrame` to trigger `moveDown` based on delta time
- Sync updates with the browser’s frame rendering
- Enable Play/Pause logic using Redux

---

## 🧩 Step 1: Add Hooks & Actions

Update your `Controls.js` imports:

```js
import React, { useEffect, useRef } from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { moveDown, moveLeft, moveRight, rotate } from '../features/gameSlice';
```

---

## 🧩 Step 2: Create Refs to Track Time

Inside the `Controls` component:

```js
const dispatch = useDispatch();
const { isRunning, speed } = useSelector((state) => state);

// Track animation frame timing
const requestRef = useRef();
const lastUpdateTimeRef = useRef(0);
const progressTimeRef = useRef(0);
```

---

## 🧩 Step 3: Add `update()` Loop

Add this inside `Controls`, before the `return`:

```js
const update = (time) => {
  requestRef.current = requestAnimationFrame(update);

  if (!isRunning) return;

  if (!lastUpdateTimeRef.current) {
    lastUpdateTimeRef.current = time;
  }

  const deltaTime = time - lastUpdateTimeRef.current;
  progressTimeRef.current += deltaTime;

  if (progressTimeRef.current > speed) {
    dispatch(moveDown());
    progressTimeRef.current = 0;
  }

  lastUpdateTimeRef.current = time;
};
```

✅ This tracks time and triggers `moveDown()` only when enough time has passed (based on `speed` from Redux).

---

## 🧩 Step 4: Use `useEffect` to Start Timer

Still inside `Controls.js`:

```js
useEffect(() => {
  requestRef.current = requestAnimationFrame(update);
  return () => cancelAnimationFrame(requestRef.current);
}, [isRunning]);
```

✅ The game now automatically moves blocks downward — and stops if paused.

---

## 🧩 Step 5: Handle Pause & Resume in Reducer

Open `gameSlice.js` and update the reducer:

```js
pause: (state) => {
  state.isRunning = false;
  return state;
},

resume: (state) => {
  state.isRunning = true;
  return state;
},
```

✅ Your existing Play/Pause button now controls the timer and gameplay.

---

## 🖼️ Final Product

You should see blocks fall at 1-second intervals and stop when paused:  
![paused](assets/paused.png)

---

## 💬 Try This

- Adjust the `speed` value in `defaultState()` to `200` for faster drops
- Log `deltaTime` to the console to see how long each frame takes

---

## 🤖 AI Prompts

> "What’s the difference between `setInterval` and `requestAnimationFrame`?"

> "Why does changing a `useRef` value not cause a re-render?"

> "How could this game speed up over time?"

> "Is there a useTimer or useInterval hook? if not how could I write one for myself?"

> "What is stale closure, and how might that affect this app?"

---

## 🧠 Check for Understanding

- Why do we reset `progressTimeRef.current` after dispatching?
- What happens if you forget to cancel `requestAnimationFrame`?
- What’s the benefit of using delta time?

---

## ✅ Commit Your Work

```bash
git add .
git commit -m "timer created"
git push
```
