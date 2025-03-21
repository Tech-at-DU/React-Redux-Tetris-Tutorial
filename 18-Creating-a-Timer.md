# ⏱️ P18 – Creating a Timer

Now that pieces can move manually, let’s create an automated **game loop** that drops the current piece over time.

You’ll:
✅ Use `useEffect` and `setInterval` to simulate a game tick  
✅ Dispatch `moveDown` on every tick  
✅ Control timer start/stop with game state

---

## 1️⃣ Add Timer Logic to `TetrisGame`
At the top:
```js
import { useEffect, useRef } from "react";
```

In the component body:
```js
const intervalRef = useRef(null);
```

Then add an effect to start/stop the timer:

```js
useEffect(() => {
  if (isRunning) {
    intervalRef.current = setInterval(() => {
      dispatch(moveDown());
    }, 1000); // drop every 1s
  } else {
    clearInterval(intervalRef.current);
  }

  return () => clearInterval(intervalRef.current);
}, [isRunning, dispatch]);
```

✅ The game now runs in real time when started!

💡 **AI Prompt:** "How can I throttle updates with setInterval in React without causing stale closures?"

---

## 2️⃣ Update Game Speed Based on Level (Optional)
To make the game faster as you level up:
```js
const speed = 1000 - level * 100;
```
Use this value instead of `1000` inside your interval.

✅ As the player clears lines and levels up, blocks drop faster!

---

## 🧠 Stretch Challenges
- [ ] Add pause/resume control for the timer
- [ ] Use `requestAnimationFrame` for smoother updates
- [ ] Create a "soft drop" mode when ⬇️ is held

---

## ➡️ Next Step
You now have an automated dropping game! In [P19 – Game Over and Restart](../P19-Game-Over-and-Restart), you’ll detect when the game should end and show a replay option.

