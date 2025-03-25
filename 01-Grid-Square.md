## 🟦 P01 – Grid Square

Let’s build the foundation of the Tetris board: a single grid square.

---

### 🎯 Goal

Create a `GridSquare` component that displays a colored square using CSS custom properties and classes like `color-1`, `color-2`, etc.

---

### 🧩 Step 1: Make the Component

Create `src/components/GridSquare.js`:

```js
import React from 'react';

// Represents a grid square with a color
export default function GridSquare({ color }) {
  const classes = `grid-square color-${color}`;

  return <div className={classes} />;
}
```

✅ This component receives a number and turns it into a class like `color-3`.

---

### 🧩 Step 2: Add Color Variables to CSS

Open `src/index.css` and add the following to define the color palette and CSS variables:

```css
:root {
  --bg-color: rgba(150, 150, 150, 1);
  --border-left-color: rgba(255, 255, 255, 0.20);
  --border-top-color: rgba(255, 255, 255, 0.33);
  --border-right-color: rgba(0, 0, 0, 0.15);
  --border-bottom-color: rgba(0, 0, 0, 0.5);
  --color-0: #eaeaea;
  --color-1: #ff6600;
  --color-2: #eec900;
  --color-3: #0000ff;
  --color-4: #cc00ff;
  --color-5: #00ff00;
  --color-6: #66ccff;
  --color-7: #ff0000;
  --tile-size: 20px;
  --border-width: 5px;
  --cols: 10;
}
```

---

### 🧩 Step 3: Define Color Classes

Still in `index.css`, add:

```css
.color-0 { background-color: var(--color-0); }
.color-1 { background-color: var(--color-1); }
.color-2 { background-color: var(--color-2); }
.color-3 { background-color: var(--color-3); }
.color-4 { background-color: var(--color-4); }
.color-5 { background-color: var(--color-5); }
.color-6 { background-color: var(--color-6); }
.color-7 { background-color: var(--color-7); }
```

---

### 🧩 Step 4: Style the Grid Square

Still in `index.css`, add:

```css
.grid-square {
  border-style: solid;
  width: var(--tile-size);
  height: var(--tile-size);
  border-width: var(--border-width);
  border-left-color: var(--border-left-color);
  border-top-color: var(--border-top-color);
  border-right-color: var(--border-right-color);
  border-bottom-color: var(--border-bottom-color);
}
```

---

### 🧩 Step 5: Render the GridSquare

Update `App.js`:

```js
import React from 'react';
import './App.css';
import GridSquare from './components/GridSquare';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <h1 className="App-title">Tetris Redux</h1>
      </header>
      <GridSquare color="1" />
    </div>
  );
}

export default App;
```

✅ You should now see an orange square (`color-1`).

---

### 💬 Try This

- Change the `color` prop to another number (0–7) and observe the result.

---

### 🤖 AI Prompts

> "Why is the `color-${color}` string a useful pattern in React components?"

> "What are CSS custom properties?"

> "How are CSS custom properties used in the code above <include CSS from above>"

---

### 🧠 Check for Understanding

- What’s the role of the `GridSquare` component in the game?
- How are props used to make it reusable?
- What does `--tile-size` do, and where is it used?

---

### 📦 Commit Your Work  
  ```bash
  git add .
  git commit -m "Added grid square"
  git push
  ```
