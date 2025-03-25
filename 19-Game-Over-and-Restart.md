## 💀 P19 – Game Over and Restart

Let’s add **game over detection** and let the player **restart** the game from the beginning.

---

### 🎯 Goal

- Detect when a piece reaches above the board
- Disable controls on game over
- Restart the game with the “Restart” button

---

## 🧩 Step 1: Add `gameOver` to Controls

In `Controls.js`, get `gameOver` from state:

```js
const { isRunning, speed, gameOver } = useSelector(state => state);
```

Then update all four control buttons to:

```jsx
<button
  disabled={!isRunning || gameOver}
  className="control-button"
  onClick={() => dispatch(moveLeft())}
>
  Left
</button>
```

✅ Do this for `Left`, `Right`, `Rotate`, and `Down`.

---

## 🧩 Step 2: Update `addBlockToGrid`

In `utils/index.js`, update the function so it checks if any block is placed **off the top of the screen** (y < 0):

```js
export const addBlockToGrid = (shape, grid, x, y, rotation) => {
  let gameOver = false;
  const block = shapes[shape][rotation];
  const newGrid = [...grid];

  for (let row = 0; row < block.length; row++) {
    for (let col = 0; col < block[row].length; col++) {
      if (block[row][col]) {
        const yIndex = row + y;
        if (yIndex < 0) {
          gameOver = true;
        } else {
          newGrid[yIndex][col + x] = shape;
        }
      }
    }
  }

  return { newGrid, gameOver };
};
```

✅ If any part of the shape is placed off-screen at the top, `gameOver` becomes `true`.

---

## 🧩 Step 3: Update `moveDown` Reducer

In `gameSlice.js`, change `moveDown` to use the new return value from `addBlockToGrid`:

```js
moveDown: (state) => {
  const { x, y, shape, grid, rotation, nextShape } = state;
  const maybeY = y + 1;

  if (canMoveTo(shape, grid, x, maybeY, rotation)) {
    state.y = maybeY;
    return state;
  }

  const { newGrid, gameOver } = addBlockToGrid(shape, grid, x, y, rotation);

  if (gameOver) {
    state.gameOver = true;
    return state;
  }

  state.grid = newGrid;
  state.x = 3;
  state.y = -4;
  state.rotation = 0;
  state.shape = nextShape;
  state.nextShape = randomShape();

  if (!canMoveTo(state.shape, newGrid, state.x, state.y, 0)) {
    state.gameOver = true;
    return state;
  }

  state.score += checkRows(newGrid);
  return state;
}
```

✅ This locks blocks, spawns new ones, and stops the game if needed.

---

## 🧩 Step 4: Implement `restart`

In `gameSlice.js`, update the restart action:

```js
restart: () => defaultState()
```

✅ This resets the game by reinitializing the state.

---

### 🖼️ What You Should See

When blocks reach the top:
- Message shows “Game Over”
- Controls are disabled
- Clicking “Restart” starts a new game

---

## 💬 Try This

- Force a game over by changing `y: 10` in `defaultState`
- Use the dev tools to set `gameOver: true` and see if buttons disable
- Add a console log to `moveDown` to watch its flow

---

## 🤖 AI Prompts

> "Why do we use `yIndex < 0` to detect game over?"

> "What’s the difference between game over and paused state in this app?"

> "What would you change to show a high score or leaderboard?"

---

## 🧠 Check for Understanding

- What causes the game to stop in `moveDown`?
- How do `addBlockToGrid` and `checkRows` work together?
- What does `defaultState()` return?

---

## ✅ Commit Your Work

```bash
git add .
git commit -m "game over and restart implemented"
git push
```

---

🎉 **Congrats! You now have a fully functioning Tetris game built with React and Redux.** 

Stretch Challenges! 