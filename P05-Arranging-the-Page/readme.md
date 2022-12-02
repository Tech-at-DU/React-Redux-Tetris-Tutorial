Arranging the Page

1. ~~Implement the overall grid square~~
1. ~~Implement the game board~~
1. ~~Implement the "next block" area~~
1. ~~Implement the score board~~
1. **Arrange the layout of the game**
    1. **Defining a CSS grid with rows and columns**
    1. **Style the grid**
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

Arranging the large UI elements on the page will make the app easier to understand and look better.

![css-grid](assets/css-grid.png)

CSS Grid was good for arranging the tiles in the grid. CSS Grid can also be used to arrange the larger UI element on the page as a whole!

CSS Grid gives you control to arrange elements on a two dimensional grid. Elements can occupy multiple rows and/or columns. All of this is easily accomplished using a simple declarative approach.

A grid is a two dimensional structure of columns and rows.

**Columns span vertically and rows span horizontally.**

In CSS we define the number of rows and columns, and the width of each column and the height of each row.

The size of a column or row can be defined in any unit supported by CSS: `%`, `px`, `em`, `pt`, `mm`, `in`, cm etc.

Columns and rows can also also be specified as a fraction of the available space with special unit: `fr`.

The CSS grid module provides properties that allow you to define the configuration of the grid many different ways. This discussion will focus on **Grid Areas**. Grid Areas are named collections of cells on the grid.

# Defining a CSS grid with rows and columns

For the Tetris UI the grid might have three columns and three rows. This layout includes the Header, NextBlock, GridBoard, ScoreBoard, Buttons components.

Let's define some requirements for this grid:

## Column Requirements

- The Header will span all of the columns along the top.
- The NextBlock, GridBoard, and ScoreBoard will be side by side each taking a column.
- The Buttons will sit in the center column below the GridBoard.
- The size of the columns can be based on the size of the game tiles (20px).
- The columns will be 80px (20px * 4 columns), 200px (20px * 10 columns), and 80px

![columns](./assets/tetris-grid-columns.png)

## Row Requirements

- There will be three rows.
The top will 100px this will contain the Header.
- The center row will be sized to fit the game grid 360px (20px * 18) -- The bottom row will hold the buttons (which haven't been made yet) 100px.

![rows](./assets/tetris-grid-rows.png)

## Columns + Rows

Put these together and they look like this:

![Columns and Rows](./assets/tetris-grid-cols-rows.png)

The intersection of Columns and Rows makes the **Grid Cells**.

![Cells](./assets/tetris-grid-cells.png)

CSS Grid allows you to define **Grid Areas** that span multiple Columns and Rows.

**The goal of the final layout is to place the header across the top three columns.**

![rows](./assets/tetris-grid-areas.png)

The image shows 5 areas defined.

- **Header:** displays the title
- **Next:** Shows the next block
- **Grid:** Shows the game grid
- **Score:** Shows the game score
- **Buttons:** Shows the game buttons

Notice the cells in the lower left and right corner are not being used.

The gap between cells is an option that can be set with CSS Grid. You will make that the same size as one grid square.

# Style The Grid

Now that You have a better sense of how grids work, let's define some styles to declare the main app container as a grid. This will layout it's children as grid items.

Currently the app structure looks looks like this:  

- div.App
  - header.App-header
  - div.grid-board
  - div.next-block
  - div.score-board

You will declare `.App` as a grid container and define some grid areas. The areas are just strings, and we'll use the following names to represent the areas:

- h : Header
- l : Left
- c : Center
- r : Right
- b : Buttons
- . : Is used to mark an empty cell

Add the following to `/src/index.css`:

```CSS
/* App */
.App {
  --col-side: calc(var(--tile-size) * 4);
  --col-center: calc(var(--tile-size) * 10);
  --grid-height: calc(var(--tile-size) * 18);

  width: calc(var(--tile-size) * (4 + 1 + 10 + 1 + 4));
  margin: auto;
  display: grid;

  grid-gap: var(--tile-size) var(--tile-size);
  /* Defines three columns of `--col-side`, `--col-center`, and `--col-side` widths. */
  grid-template-columns: var(--col-side) var(--col-center) var(--col-side);
  /* Defines three rows of `100px`, `--grid-height`, and 100px. */
  grid-template-rows: 100px var(--grid-height) 100px;

/* This defines the areas on the grid with names: 'h', 'l', 'c', 'r',
and 'b'. The '.' represents an empty cell on the grid. */
  grid-template-areas: "h h h"
                       "l c r"
                       ". b .";
}
```

It's starting to look like a grid but things are not where you want them. The following steps map each element to it's location defined in `grid-template-areas`.

Now let's assign child elements to grid areas in the parent.

Assign the header a grid area by adding the following to `/src/index.css`

```CSS
/* App-header */
.App-header {
  grid-area: h;
}
```

Let's *edit* some of the previous styles we made to include the `grid-area`

Add the last line to the `.next-block` rule in `/src/index.css`:

```CSS
/* Next Block */
.next-block {
  ...
  grid-area: l; /* Grid area l left column */
}
```

Add the last line to the `.grid-board` rule in `/src/index.css`:

```CSS
/* Grid Board */
.grid-board {
  ...
  grid-area: c; /* Assign to grid area c */
}
```

Finally, assign a `grid-area` for `.score-board` in `/src/index.css`:

```CSS
/* score-board */
.score-board {
  grid-area: r;
}
```

# Product So Far

Check out your browser now, sure looks a lot better than before!

![grid-area](assets/grid-area.png)

# Now Commit

```bash
$ git add .
$ git commit -m 'Added grid area styles'
$ git push
```

Great work! From this chapter, we were able to **create complex layouts with CSS grid!**

## Resources

- https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template-areas
