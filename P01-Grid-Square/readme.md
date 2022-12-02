# Tetris Grid

1. **Implement the overall grid square**
    1. **Build the grid square component**
    1. **Add styling**
1. Implement the game board
1. Implement the "next block" area
1. Implement the score board
1. Arrange the layout of the game
1. Implement the controls
1. Implement the message popup
1. Implement the actions and reducers
1. Do some code organizing and cleanup
1. Implement state and shapes
1. Connect each component up to state and reducers
1. Implement block rotation
1. Implement moving blocks
1. Building a timer system
1. Implementing Game Over and Restart

In this section you will make a component that represents a single grid square. The game board is played on a grid made up of many grid squares.

One square will look like this:

![square](assets/square.png)

The game will be made up of 180 squares in different colors.

![squares](assets/squares.png)

Colors will be stored as an index:

- Color 0: ![square](assets/square-0.png)
- Color 1: ![square](assets/square-1.png)
- Color 2: ![square](assets/square-2.png)
- Color 3: ![square](assets/square-3.png)
- Color 4: ![square](assets/square-4.png)
- Color 5: ![square](assets/square-5.png)
- Color 6: ![square](assets/square-6.png)
- Color 7: ![square](assets/square-7.png)

The grid square is a component. 

# Why Use Components

React uses a component based architecture. Everything you see rendered in the browser is a component.

Breaking components down into smaller and more granular components is usually the best strategy with React. While you could make the game from a single Game Component. A better strategy would be to make a game from many components that all fit together like Lego brocks to form the final game.

Each component will require CSS styles. The components used in this project will not have much use in other projects. They are too specialized. This makes keeping all of the styles in a single stylesheet more convenient.

# Make the GridSquare Component

This component will render as a single square of color.

Make a new file: `src/components/GridSquare.js` with the following code:

```js
import React from 'react'

// Represents a grid square with a color

export default function GridSquare({ color }) {
  const classes = `grid-square color-${color}`
  return <div className={ classes } />
}
```

The GridSquare is just a `div` with some class names. Below is a breakdown of the class names:

- `GridSquare` : A function that defines the `GridSquare` component. All grid squares will use this definition. We pass props to a component to configure it. 
- Notice on the first line you have deconstructed props into `color` here: `GridSquare({ color })`
- `color-${color}` : The color of the square will be
passed via props. The value of `color` will be a number e.g. 1, 2, 3.
- Note! The classes string will contain something like this: `grid-square color-3`. When used as class name this will be read as two classes: `grid-square` and `color-3`. In this way you will apply styles shared by all grid squares with the `grid-square` class and set the color for each square with the `color-#` class. 

**As a requirement The class name for any grid square will use the following format:** `color-0`, `color-1`, `color-2`, `color-3` etc.

You'll define these color classes later in the tutorial.

# Define some CSS

This project will store all of it's styles in `index.css`. **The components in the project are not portable, they would find little use outside of this project.**

First we should edit the `min-height` of `.App-header` in `/src/App.css` so that it's not taking up the whole page anymore:

```css
.App-header {
  background-color: #282c34;
  min-height: 10vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: calc(10px + 2vmin);
  color: white;
}
```

Now you can edit `/src/index.css` to include the below styles that define some properties for the colors and sizes we'll use:

```css
:root {
  --bg-color: rgba(150, 150, 150, 1);

  /* Border Colors are all transparent colors. These will tint or shade the background color of the square. */
  --border-left-color: rgba(255, 255, 255, 0.20);
  --border-top-color: rgba(255, 255, 255, 0.33);
  --border-right-color: rgba(0, 0, 0, 0.15);
  --border-bottom-color: rgba(0, 0, 0, 0.5);

  /* Square Colors:  background colors for the squares.*/
  --color-0: #eaeaea;
  --color-1: #ff6600;
  --color-2: #eec900;
  --color-3: #0000ff;
  --color-4: #cc00ff;
  --color-5: #00ff00;
  --color-6: #66ccff;
  --color-7: #ff0000;

  /* Button Colors */
  --button-color-t: rgba(200, 200, 200, 1);
  --button-color-r: rgba(150, 150, 150, 1);
  --button-color-b: rgba(120, 120, 120, 1);
  --button-color-l: rgba(222, 222, 222, 1);

  /* Numbers define values that will be used throughout the CSS.
  --tile-size: 20px for example will set size of the grid squares. */
  --cols: 10;
  --rows: 18;
  --tile-size: 20px;
  --border-width: 5px;
}
```

# Color Classes

The colors will be assigned to grid squares as classes.
With class names: `color-0`, `color-1`, `color-2` etc.
You will define these classes using the color variables you set earlier.

Add the following below the code you just added to `/src/index.css`:

```css
/* Colors */
.color-0 {
  background-color: var(--color-0);
}

.color-1 {
  background-color: var(--color-1);
}

.color-2 {
  background-color: var(--color-2);
}

.color-3 {
  background-color: var(--color-3);
}

.color-4 {
  background-color: var(--color-4);
}

.color-5 {
  background-color: var(--color-5);
}

.color-6 {
  background-color: var(--color-6);
}

.color-7 {
  background-color: var(--color-7);
}
```

With this arrangement you can use the colors anywhere in your
stylesheet. You can also make global changes to colors in
one location.

These changes won't make much visual change to the project so far. You need to put these in place so things can happen in the future! 

# Grid Square Appearance

Now you need to define the appearance of a grid square. The grid squares all have a border style, and a width and a height. By defining these as variables it will be easier to make changes to the appearance of the grid squares through the variables at the top of the stylesheet.

Add the following to `/src/index.css`:

```css
/* Grid Square */
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

That might seem like a lot of styles but much of what is there will be reused throughout this tutorial. With this arrangement you can easily make changes to the size and border in a single place, at the top of the style sheet.

Defining these CSS custom properties is well worth the time effort your future self will thank you!

## Note about CSS custom properties

CSS custom properties, if you are not familiar, are variables that you define in CSS. Custom property names must begin with a double hyphen: `--`. For example: 

- `--tile-size`
- `--color-1`
- `--border-width`
- etc. 

You can assign any valid CSS value to a custom property! 

To access the value of a custom property you must use the `var()` function, awkward, I know. But that's how it works for some examples take a look at the code you just added: 

```CSS
:root {
  ...
  --tile-size: 20px; /* Sets the --tile-size */
  ...
}

.grid-square {
  ...
  width: var(--tile-size); /* Applies the value of --tile-size */
  ...
}

```

# Test a Grid Square

Modify `/src/App.js` as shown below:

```js
import React from 'react';
import './App.css';

import GridSquare from './components/GridSquare'

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

Here you added the game title in the header. Then made an instance of the `GridSquare` component. It should show a single square. Since you configured the GridSquare with color=1 it should use the color defined in your stylesheet as `color-1` which is orange. 

Setting the color to 1 should display an orange square:

![orange](assets/orange-square.png)

Try some other values by changing the value of `color`.

# Now Commit

```bash
$ git add .
$ git commit -m 'Added grid square'
$ git push
```

We got some great practice with starting to **use CSS variables!** We'll be using these more throughout this tutorial.

## Resources

- https://developer.mozilla.org/en-US/docs/Web/CSS/
- https://www.quackit.com/css/css_color_codes.cfm
