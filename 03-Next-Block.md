## 🔷 P03 – Next Block

Let’s display the "next block" preview — a 4×4 grid that shows which block will drop next.

---

### 🎯 Goal

- Create a `NextBlock` component that uses a 4×4 grid of `GridSquare`s.
- Style the grid and add it to the UI.

---

### 🧩 Step 1: Create the Component

Make a new file: `src/components/NextBlock.js`

```js
import React from 'react';
import GridSquare from './GridSquare';

// Draws the "next" block view showing the next block to drop
export default function NextBlock() {
  const block = [
    [0, 0, 0, 0],
    [0, 0, 0, 0],
    [0, 0, 0, 0],
    [0, 0, 0, 0],
  ];

  const grid = block.map((rowArray, row) =>
    rowArray.map((square, col) => (
      <GridSquare key={`${row}${col}`} color={square} />
    ))
  );

  return <div className="next-block">{grid}</div>;
}
```

✅ This uses nested `.map()` calls to render the 4×4 block using `GridSquare`.

---

### 🧩 Step 2: Add Styles

Update `src/index.css`:

```css
/* Next Block */
.next-block {
  display: grid;
  grid-template-columns: repeat(4, var(--tile-size));
  align-self: flex-start;
}
```

This arranges the 4×4 grid nicely using CSS Grid.

---

### 🧩 Step 3: Add to App

Update `src/App.js`:

```js
import React from 'react';
import './App.css';

import GridBoard from './components/GridBoard';
import NextBlock from './components/NextBlock';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <h1 className="App-title">Tetris Redux</h1>
      </header>
      <GridBoard />
      <NextBlock />
    </div>
  );
}

export default App;
```

✅ You should now see the 10×18 game grid and the 4×4 next block preview.

---

### 💬 Try This

- Change a few `0`s in the `block` array to `1`, `2`, or `3` to preview different colored blocks.
- Add a border or background to `.next-block` to help visualize layout.

---

### 🤖 AI Prompts

> "How do the nested `.map()` calls in `NextBlock` generate a flat list of components?"

> "Can you refactor `NextBlock` to accept a block array as a prop?"

---

### 🧠 Check for Understanding

- Why is `.next-block` styled with `grid-template-columns: repeat(4, ...)`?
- What happens if the `block` array is not 4×4?
- How are `key`s important in the nested `.map()`?

---

### ✅ Commit Your Progress

```bash
git add .
git commit -m "Added initial next block"
git push
```
