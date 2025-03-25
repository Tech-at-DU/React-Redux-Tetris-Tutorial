## ⚙️ P08 – Actions & Reducers (Redux Setup)

Let’s start managing game state with **Redux Toolkit**. This will let us control the game grid, block movement, game status, and more.

---

### 🎯 Goal

- Install and configure Redux Toolkit
- Create a Redux store and connect it to React
- Create a `gameSlice` with placeholder actions and reducers

---

### 🧩 Step 1: Install Dependencies

```bash
npm install @reduxjs/toolkit react-redux
```

---

### 🧩 Step 2: Create the Redux Store

Create a new folder: `src/app`  
Then create: `src/app/store.js`

```js
import { configureStore } from '@reduxjs/toolkit';

export const store = configureStore({
  reducer: {},
});
```

✅ This sets up the store. We’ll add real reducers soon.

---

### 🧩 Step 3: Wrap App in Redux Provider

Edit `src/index.js`:

```js
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

import { store } from './app/store';
import { Provider } from 'react-redux';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>
);
```

✅ Now all components can access state via `useSelector()` and dispatch actions with `useDispatch()`.

---

### 🧩 Step 4: Define a Slice

Create a folder: `src/features`  
Then create: `src/features/gameSlice.js`

```js
import { createSlice } from '@reduxjs/toolkit';

export const gameSlice = createSlice({
  name: 'game',
  initialState: {},
  reducers: {
    pause: () => {},
    resume: () => {},
    moveLeft: () => {},
    moveRight: () => {},
    moveDown: () => {},
    rotate: () => {},
    gameOver: () => {},
    restart: () => {},
  },
});

// Action creators
export const {
  moveLeft,
  moveRight,
  moveDown,
  rotate,
  pause,
  resume,
  gameOver,
  restart
} = gameSlice.actions;

export default gameSlice.reducer;
```

✅ You now have action creators and reducer placeholders — logic will be added later.

---

### 🧩 Step 5: Connect Slice to Store

Update `src/app/store.js`:

```js
import { configureStore } from '@reduxjs/toolkit';
import gameReducer from '../features/gameSlice';

export const store = configureStore({
  reducer: gameReducer,
});
```

✅ No more reducer errors — Redux is now fully wired up.

---

### 💬 Try This

- Log `store.getState()` in the console and see what it returns.
- Add a temporary reducer that logs something when triggered.

---

### 🤖 AI Prompts

> "What’s the purpose of `createSlice()` in Redux Toolkit?"

> "How do `actions` and `reducers` work together in Redux?"

> "Can you describe the difference between `state`, `action`, and `dispatch`?"

---

### 🧠 Check for Understanding

- What does `Provider` do?
- What are the three main parts of a `slice`?
- What happens if you don’t export your reducer correctly?

---

### ✅ Commit Your Work

```bash
git add .
git commit -m "Added initial actions and reducer"
git push
```
