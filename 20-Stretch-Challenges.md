## 🎯 Tetris Redux Stretch Challenges

You've built a fully working version of Tetris — nice work! But there's plenty of room to **customize, extend, and deepen** your understanding of how the game (and Redux!) works under the hood.

Try some of these **stretch goals** to level up your skills:

---

## 🎨 1. Restyle the Game

The current styles mimic the original NES version of Tetris, which… let’s be honest… looks a bit dated.

### 💡 Challenge:
- Redesign the game UI using modern styling
- Try CSS custom properties, gradients, or even a glassmorphism effect
- Make the grid and blocks pulse, animate, or glow
- Use a font and color scheme that feels *you*
- There are plenty of other details about the design that can be improved!

### 🚀 Stretch It Further:
- Add a dark mode

---

## ⌨️ 2. Add Keyboard Controls

Right now, the player controls the blocks using on-screen buttons. Let’s add **keyboard support** for a more fluid gameplay experience.

### 💡 Challenge:
- Use `useEffect` to listen for `keydown` events
- Map the **arrow keys**:
  - `←` – move left
  - `→` – move right
  - `↓` – move down faster
  - `↑` or `space` – rotate

### 🚀 Stretch It Further:
- Add **soft drop** and **hard drop** (press down to speed up, space to drop instantly)
- Let players remap their controls
- Add sound effects on key presses

---

## 📈 3. Add Levels & Speed Progression

Tetris gets faster as you score points. Let’s build a **level system** that speeds up the game as the player progresses.

### 💡 Challenge:
- Create a `level` property in your state
- Increase level every time the player clears 10 lines
- Decrease the `speed` state to make blocks fall faster. You'll need to remove timer and start a new timer with the updated interval. 

### 🚀 Stretch It Further:
- Display the current level on the scoreboard
- Add new background colors or music on each level
- Implement **challenge levels**: pre-filled grids, reversed controls, etc.

---

## 🧠 Bonus Ideas

If you're looking for even more challenges...

### 🔁 Implement Hold & Swap
- Add a space for a **"held" piece**
- Let the player press a key to store or swap their current piece

### 🧮 Add a High Score System
- Save the player's highest score using `localStorage`
- Create a leaderboard and allow name input

### 📱 Make It Mobile-Friendly
- Add swipe gestures for movement and rotation
- Adjust the layout and scale for smaller screens

### 🌐 Publish It
- Deploy the project with Vercel, Netlify, or GitHub Pages
- Share it with friends — or put it in your portfolio!

---

## 💬 Reflect & Share

Once you've finished a stretch challenge:

- Write a blog post or tweet about what you built
- Teach a friend how the game works
- Fork your project and start turning it into something totally new (Puzzle mode? Multiplayer? Tetris RPG?)

---

### 🧠 Final Thought

The best part of building games is that you’re always **1 idea away** from something amazing. Start with one stretch goal — then stretch further.

You've got the foundation. Now make it yours. 🎮✨
