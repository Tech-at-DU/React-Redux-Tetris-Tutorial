# 🟥 P19 – Game Over and Restart

With your timer and gameplay loop in place, let’s implement **game over detection** and a clean way to **restart the game**.

You’ll:
✅ Check for collisions at the top of the board  
✅ Dispatch a `endGame()` action if game over  
✅ Let the player restart from the `MessagePopup`

---

## 1️⃣ Add Game Over Check in moveDown Reducer
In `gameSlice.js`, update your `moveDown` reducer:

```js
moveDown(state) {
  const { position, shape } = state.currentPiece;
  const newRow = position.row + 1;

  if (collisionDetected(state.board, shape, { ...position, row: newRow })) {
    // Game over if collision occurs at top
    if (position.row === 0) {
      state.gameOver = true;
      state.isRunning = false;
    }
    return;
  }

  state.currentPiece.position.row = newRow;
}
```

✅ This ends the game if a new piece collides immediately.

---

## 2️⃣ Create `collisionDetected()` Utility
In `gameUtils.js`:

```js
export function collisionDetected(board, shape, position) {
  return shape.some((row, rIdx) =>
    row.some((cell, cIdx) => {
      if (!cell) return false;

      const rowPos = position.row + rIdx;
      const colPos = position.col + cIdx;

      return (
        rowPos >= board.length ||
        colPos < 0 ||
        colPos >= board[0].length ||
        board[rowPos]?.[colPos]?.color !== "#000"
      );
    })
  );
}
```

✅ Detects boundary or overlap collisions.

---

## 3️⃣ Let Player Restart from MessagePopup
In `MessagePopup.js`, update the component:

```jsx
const MessagePopup = ({ message, isVisible, onPlayAgain }) => {
  if (!isVisible) return null;

  return (
    <div className="popup-overlay">
      <div className="popup-content">
        <h2>{message}</h2>
        {message === "Game Over" && (
          <button onClick={onPlayAgain}>Play Again</button>
        )}
      </div>
    </div>
  );
};
```

Then pass in a `handleRestart()` callback from `TetrisGame.js`:

```js
const handleRestart = () => {
  dispatch(startGame());
};

<MessagePopup
  message={message}
  isVisible={showPopup}
  onPlayAgain={handleRestart}
/>
```

✅ You can now replay the game after a game over!

💡 **AI Prompt:** "How do I detect collisions between falling blocks and the board in Tetris?"

---

## 🧠 Stretch Challenges
- [ ] Show a final score and high score before restarting
- [ ] Add a countdown before replay starts
- [ ] Animate the game over message with scale or fade

---

## ✅ Final Gameplay Checkpoint
You now have:
- Piece rotation and movement
- Live score tracking
- Game over detection
- Timer-based gameplay loop
- Restart functionality

In the final page, we’ll wrap up the project in [P20 – Final Thoughts](../P20-Final-Thoughts)!

