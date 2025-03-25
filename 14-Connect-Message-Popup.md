## 💬 P14 – Connect Message Popup

Let’s wire up the `MessagePopup` so it shows when the game is **paused** or **over**, and hides otherwise.

---

### 🎯 Goal

- Access `isRunning` and `gameOver` from Redux
- Dynamically show or hide the message popup
- Display appropriate message text

---

### 🧩 Step 1: Connect to Redux

Open `src/components/MessagePopup.js` and import:

```js
import { useSelector } from 'react-redux';
```

Then, get the state values inside the component:

```js
const { isRunning, gameOver } = useSelector((state) => state);
```

✅ You now have access to the game’s status.

---

### 🧩 Step 2: Conditionally Show the Popup

Use logic to show the popup and change the message:

```js
let message = '';
let isHidden = 'hidden';

if (gameOver) {
  message = 'Game Over';
  isHidden = '';
} else if (!isRunning) {
  message = 'Paused';
  isHidden = '';
}
```

✅ When the game is paused or over, the popup appears. Otherwise, it’s hidden.

---

### 🧩 Step 3: Final Component Code

```js
import React from 'react';
import { useSelector } from 'react-redux';

export default function MessagePopup() {
  const { isRunning, gameOver } = useSelector((state) => state);

  let message = '';
  let isHidden = 'hidden';

  if (gameOver) {
    message = 'Game Over';
    isHidden = '';
  } else if (!isRunning) {
    message = 'Paused';
    isHidden = '';
  }

  return (
    <div className={`message-popup ${isHidden}`}>
      <h1>{message}</h1>
    </div>
  );
}
```

✅ You’re now conditionally showing messages based on game state using Redux.

---

### 💬 Try This

- Temporarily set `isRunning: false` or `gameOver: true` in `defaultState()` to test different messages.
- Change the CSS for `.message-popup` or `.hidden` to visualize behavior more clearly.

---

### 🤖 AI Prompts

> "Why is `useSelector` more flexible than passing props down to `MessagePopup`?"

> "What are other ways to conditionally render components in React?"

> "How would you animate the appearance of this popup with CSS or a library like Framer Motion?"

---

### 🧠 Check for Understanding

- What’s the role of the `hidden` class?
- What happens if both `isRunning` and `gameOver` are false?
- Why don’t we need to pass anything to `MessagePopup` via props?

---

### ✅ Commit Your Work

```bash
git add .
git commit -m "Added connection for message popup"
git push
```
