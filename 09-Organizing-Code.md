# 🗂️ P09 – Organizing Code

As your Tetris app grows, it’s essential to keep your codebase **clean and modular**. In this step, you’ll:
✅ Restructure your files into logical folders  
✅ Group features by responsibility (Redux slices, components, utils)  
✅ Prepare the app for future development

---

## 🧱 Step 1: Suggested Folder Structure
Here’s a recommended layout for your project:

```
src/
├── app/
│   └── store.js
├── components/
│   ├── Controls.js
│   ├── Controls.css
│   ├── GridBoard.js
│   ├── GridSquare.js
│   ├── MessagePopup.js
│   ├── NextBlock.js
│   ├── ScoreBoard.js
│   ├── TetrisGame.js
│   └── ...
├── features/
│   └── game/
│       ├── gameSlice.js
│       ├── gameUtils.js
│       └── pieceShapes.js
├── utils/
│   └── formatScore.js (optional)
├── App.js
└── index.js
```

✅ **Benefits of this layout:**
- `components/`: All reusable and visual components
- `features/game/`: Game state logic, reducers, and related utilities
- `app/`: Redux store and configuration
- `utils/`: Helper functions that aren’t tied to state or UI

💡 **AI Prompt:** "What are the benefits of feature-based folder structures in React?"

---

## 📁 Step 2: Move Files Into Structure
Go ahead and move your files according to the layout above. Then, update all imports accordingly. For example:

```js
// BEFORE
import ScoreBoard from "./ScoreBoard";

// AFTER
import ScoreBoard from "../components/ScoreBoard";
```

✅ Tip: Modern IDEs like VS Code can auto-update imports when files are moved.

---

## 🔍 Step 3: Create a `pieceShapes.js` File
Inside `features/game/`, add block shape definitions:

```js
// features/game/pieceShapes.js
export const SHAPES = {
  I: [
    [1, 1, 1, 1],
    [0, 0, 0, 0],
    [0, 0, 0, 0],
    [0, 0, 0, 0]
  ],
  O: [
    [1, 1],
    [1, 1]
  ],
  // Add other shapes: T, L, J, S, Z
};
```

✅ This prepares you for building actual gameplay in later steps.

---

## 🧠 Stretch Challenges
- [ ] Separate logic for block movement into a `movement.js` file
- [ ] Create a dedicated folder for constants (colors, key codes)
- [ ] Use TypeScript or PropTypes to add type safety

---

## ➡️ Next Step
With your code organized, you're ready to connect components to Redux and render actual game state in [P10 – Default State & Block Shapes](../P10-Default-State-and-Block-Shapes)!

