# 💬 P07 – Message Popup

In this step, you’ll build a simple popup overlay to display important game messages like:
- “Game Over”
- “Paused”
- “Ready?”

You’ll:
✅ Create a modal-like `MessagePopup` component  
✅ Style it with a semi-transparent overlay  
✅ Display different messages based on props

---

## 🧩 Step 1: Create the `MessagePopup` Component
Create a file: `src/components/MessagePopup.js`

```jsx
import React from "react";
import "./MessagePopup.css";

const MessagePopup = ({ message, isVisible }) => {
  if (!isVisible) return null;

  return (
    <div className="popup-overlay">
      <div className="popup-content">
        <h2>{message}</h2>
      </div>
    </div>
  );
};

export default MessagePopup;
```

✅ This component is conditionally rendered based on the `isVisible` prop.

---

## 🎨 Step 2: Style the Popup
Create a file: `src/components/MessagePopup.css`

```css
.popup-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.6);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.popup-content {
  background: #fff;
  padding: 40px;
  border-radius: 10px;
  text-align: center;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.3);
}

.popup-content h2 {
  font-size: 32px;
  margin: 0;
}
```

✅ The overlay is centered, responsive, and visually distinct.

---

## 🧪 Step 3: Test It in `TetrisGame`
Add this to `TetrisGame.js` to preview:

```jsx
import MessagePopup from "./MessagePopup";

<MessagePopup message="Game Over" isVisible={true} />
```

✅ **Checkpoint:** You should see a centered popup with the text "Game Over".

---

## 🧠 Stretch Challenges
- [ ] Animate the popup (fade in/out or scale)
- [ ] Add a “Play Again” button
- [ ] Use keyboard shortcuts to close the message

---

## ➡️ Next Step
In [P08 – Actions and Reducers](./08-Actions-and-Reducers.md), you’ll begin wiring up Redux state to control these interactions!

