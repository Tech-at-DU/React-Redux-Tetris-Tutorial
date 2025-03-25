## 🧹 P09 – Organizing Code

Let’s clean up and prepare for scalability by putting utility functions into their own file.

---

### 🎯 Goal

- Create a `utils` folder with general-purpose functions.
- Write a reusable `random(min, max)` function.

---

### 🧩 Step 1: Create the Utils File

Make a new file: `src/utils/index.js`  
Add this function:

```js
export const random = (min, max) => {
  return Math.floor(Math.random() * (max - min + 1)) + min;
};
```

✅ This function returns an integer between `min` and `max`, inclusive.

---

### 📦 Example Use

```js
random(1, 7); // Might return 4
```

This will be useful for selecting random blocks and shapes.

---

### 💬 Try This

- Temporarily `console.log(random(0, 3))` inside a component to test.
- What happens if `min === max`?

---

### 🤖 AI Prompts

> "Why use `Math.floor` instead of `Math.round` in a `random()` function?"

> "How could you write a function that returns a random value from an array?"

---

### 🧠 Check for Understanding

- Why is `utils/index.js` a better place for this than inside a component?
- What happens if you reverse the `min` and `max` values?

---

### ✅ Commit Your Work

```bash
git add .
git commit -m "Added utils"
git push
```
