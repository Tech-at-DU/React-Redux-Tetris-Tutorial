## 🧩 P11 – Connect Next Block

Let’s make the **NextBlock** component dynamic by pulling state from Redux. This will display a **random, colored block** each time the game starts.

---

### 🎯 Goal

- Use `useSelector` to access `nextShape` from state
- Map the 4x4 shape array to a grid of `GridSquare`s
- Match color to shape index

---

### 🧩 Step 1: Import Redux & Shapes

Open `src/components/NextBlock.js` and add:

```js
import { useSelector } from 'react-redux';
import { shapes } from '../utils';
```

---

### 🧩 Step 2: Read State with `useSelector`

Inside your `NextBlock` component, pull the `nextShape` from Redux:

```js
const nextShape = useSelector((state) => state.nextShape);
```

✅ This gives you the shape index to render.

---

### 🧩 Step 3: Get the Shape Grid

Get the first rotation of the selected shape:

```js
const block = shapes[nextShape][0]; // Always use rotation 0 for preview
```

---

### 🧩 Step 4: Map the Grid to Squares

Update the shape mapping logic:

```js
const grid = block.map((rowArray, row) =>
  rowArray.map((square, col) => {
    const color = square ? nextShape : 0;
    return <GridSquare key={`${row}${col}`} color={color} />;
  })
);
```

✅ This uses the ternary operator (`? :`) to check each square:  
If it’s 1, show the shape’s color. If 0, use gray (`color-0`).

---

### 🧩 Step 5: Final Component

Your full `NextBlock.js` should now look like:

```js
import React from 'react';
import GridSquare from './GridSquare';
import { useSelector } from 'react-redux';
import { shapes } from '../utils';

export default function NextBlock() {
  const nextShape = useSelector((state) => state.nextShape);
  const block = shapes[nextShape][0];

  const grid = block.map((rowArray, row) =>
    rowArray.map((square, col) => {
      const color = square ? nextShape : 0;
      return <GridSquare key={`${row}${col}`} color={color} />;
    })
  );

  return <div className="next-block">{grid}</div>;
}
```

✅ You now see a different colored shape every time you refresh the page.

---

### 💬 Try This

- Refresh the page several times — does the shape and color change?
- Replace `nextShape` with a fixed number (like `3`) to test a specific shape.

---

### 🤖 AI Prompts

> "I'm building an app with Redux toolkit, explain useSelector() as beginner, intermediate, and advanced."

> "Why do we use `useSelector` instead of passing props?"

> "How could this component show a *rotated* preview if needed?"

> "What happens if you try to render `shapes[0][0]`?"

---

### 🧠 Check for Understanding

- What’s the role of `nextShape` in the component?
- How do you map an array of arrays to JSX?
- Why is color tied to shape index?

---

### ✅ Commit Your Work

```bash
git add .
git commit -m "Added connection for next block"
git push
```
