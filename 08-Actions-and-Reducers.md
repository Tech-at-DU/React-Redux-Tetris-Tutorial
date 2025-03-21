# 🔄 P08 – Actions and Reducers

It’s time to start managing game logic with **Redux Toolkit**! In this step, you’ll:
✅ Define the game’s state structure  
✅ Create actions for core interactions (start, reset, pause, etc.)  
✅ Use a reducer to update the state in response to those actions

---

## 🧠 Step 1: Define Initial Game State
Create a file: `src/features/game/gameSlice.js`

```js
import { createSlice } from "@reduxjs/toolkit";

const initialState = {
  board: [],
  currentPiece: null,
  nextPiece: null,
  score: 0,
  level: 0,
  linesCleared: 0,
  gameOver: false,
  isRunning: false,
};

const gameSlice = createSlice({
  name: "game",
  initialState,
  reducers: {
    startGame(state) {
      state.board = createEmptyBoard();
      state.currentPiece = generateRandomPiece();
      state.nextPiece = generateRandomPiece();
      state.score = 0;
      state.level = 0;
      state.linesCleared = 0;
      state.isRunning = true;
      state.gameOver = false;
    },
    pauseGame(state) {
      state.isRunning = false;
    },
    resumeGame(state) {
      state.isRunning = true;
    },
    endGame(state) {
      state.gameOver = true;
      state.isRunning = false;
    },
    resetGame(state) {
      return initialState;
    },
  },
});

export const {
  startGame,
  pauseGame,
  resumeGame,
  endGame,
  resetGame,
} = gameSlice.actions;

export default gameSlice.reducer;

// Placeholder utils
function createEmptyBoard(rows = 20, cols = 10) {
  return Array.from({ length: rows }, () =>
    Array.from({ length: cols }, () => ({ color: "#000" }))
  );
}

function generateRandomPiece() {
  return { shape: [], color: "#f00" }; // Replace with real logic
}
```

📌 These actions will allow the game to transition between different play states.

💡 **AI Prompt:** “What is the purpose of a reducer in Redux, and why is immutability important?”

---

## 🧪 Step 2: Add Reducer to Store
Create (or update) your Redux store: `src/app/store.js`

```js
import { configureStore } from "@reduxjs/toolkit";
import gameReducer from "../features/game/gameSlice";

export const store = configureStore({
  reducer: {
    game: gameReducer,
  },
});
```

---

## 🧠 Stretch Challenges
- [ ] Add actions for updating the board each tick
- [ ] Add reducer logic for line clearing and scoring
- [ ] Connect game speed to `level`

---

## ➡️ Next Step
Now that your core state logic is ready, move on to [P09 – Organizing Code](../P09-Organizing-Code) to clean up and prepare for future logic!

