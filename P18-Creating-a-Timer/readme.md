# Creating a Timer

1. ~~Implement the overall grid square~~
1. ~~Implement the game board~~
1. ~~Implement the "next block" area~~
1. ~~Implement the score board~~
1. ~~Arrange the layout of the game~~
1. ~~Implement the controls~~
1. ~~Implement the message popup~~
1. ~~Implement the actions and reducers~~
1. ~~Do some code organizing and cleanup~~
1. ~~Implement state and shapes~~
1. ~~Connect each component up to state and reducers~~
1. ~~Implement block rotation~~
1. ~~Implement moving blocks~~
1. **Building a timer system**
  1. **Overview of timing and how to use `requestAnimationFrame`**
  1. **Track delta time in the GridBoard**
  1. **Build out an `update` function to update the GridBoard as blocks fall**
  1. **Implement the logic in the Pause/Resume button**
1. Implementing Game Over and Restart

With what we have so far, the game is almost finished. One important step is needed to make turn this into a playable game: the blocks need to move down on their own!

To make this work the game needs to issue `moveDown` actions on its own. The time between each of these actions will determine the difficulty.

You're going to use `requestAnimationFrame` to implement this feature. It may seem a little strange, but it has a couple of advantages over using something like `setInterval`, and is a great way to practice some new ideas.

# Dispatching a periodic MOVE_DOWN action

The goal here is to issue a `moveDown` action every time interval, where the time interval might start at once per second and decrease over time as the game is played to increase difficulty.

You're going to be referring to **Delta time** a lot in this chapter. Delta time represents the difference between now and the last time the browser redrew the window.

As usual, let's go over some basic requirements:

- The game needs to handle time and issue `moveDown`
actions at intervals.
- The interval will be the speed set on the state.
- Timing should be handled in the `GameBoard` component

You could place the timing code in the App or Controls or other Components as well.

# Request Animation Frame Overview

The browser draws the contents of the window at regular intervals, about every 16.7 milliseconds. It's advantageous to our application to update our views on the same clock.

JavaScript provides a method to notify our applications when the browser is about to redraw the screen.

[requestAnimationFrame()](https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame) is a method that takes a callback that is executed just before the browser redraws the window.

# useRef()

In React projects each time a component is rendered all of the variables in the component function is defined. That means all of the values from the last render are lost and new values are generated on a new render. 

This is a feature of Reacts virtual DOM. You can think about it like this. Imagine each component is a function, not hard to do, components are written as functions! Component functions return the HTML that they are responsible for rendering. That means that the function is run each time React needs to draw the component and all of the HTML is generated new at that time. It also means that variables are defined locally each time the function is run. That last idea is standard JS. 

There are times when you need a component to "remember" a value it used the last time it was rendered. 

React provides two hooks for this purpose. 

- `useState`
- `useRef`

The `useState` hook lets you define values that when changed will cause the component to render again. 

The `useRef` hook will hold on to a value and changing this value won't automatically render the component. 

# useEffect

The `useEffect` hook is used to handle lifecycle events for a component. 

A component is a function as such each time the component is rendered all of the code in the function is run. In some cases, you may have code that should only be run the first a component is added to the DOM, or code that is run when a component is removed from the DOM. These are lifecycle events, and `useEffect` covers these. 

# Making things move

To make things move in the game you'll combine `useRef`, `useEffect`, and `requestAnimationFrame`. 

The idea is to calculate the time between calls to `requestAnimationFrame`. When the time is greater than the speed of the game dispatch a `moveDown` action. 

This means that you'll be getting `requestAnimationFrame` updates often but changing state and rendering components less often (only when delta time is greater than the speed of the game.) 

Add the following within the `Controls` class in `/src/components/Controls.js`:

Edit your import statement at the top of the file. 

```JS 
import React, { useEffect, useRef } from 'react'
import { useSelector, useDispatch } from 'react-redux'
import { moveDown, moveLeft, moveRight, rotate } from '../features/gameSlice'
...
```

Next, define some refs. You'll three. 

- `requestRef` - Holds a referece to requestAnimationFrame
- `lastUpdateTimeRef` - tracks the time of the last update
- `progressTimeRef` - tracks the total time between updates

These are variables that will persist outside of calls to this component function. 

Add the following within the `Controls` function in `/src/components/Controls.js`:

```JS 
export default function Controls() {
  const dispatch = useDispatch()
  // Added speed here! 
  const { isRunning, speed } = useSelector(state => state)

  // Set up the game timer
  const requestRef = useRef()
  const lastUpdateTimeRef = useRef(0)
  const progressTimeRef = useRef(0)
  ...
}
```

# Adding an update function

Write a function that will handle updates from requestAnimationFrame. This function will be defined inside the `Controls` function, after the variables above, and before the return statement. 

```JS 
export default function Controls() {
  ...
  // Handle game updates to move blocks down the screen
  const update = (time) => {
    requestRef.current = requestAnimationFrame(update)
    if (!isRunning) {
      return 
    }
    if (!lastUpdateTimeRef.current) {
      lastUpdateTimeRef.current = time
    }
    const deltaTime = time - lastUpdateTimeRef.current
    progressTimeRef.current += deltaTime
    if (progressTimeRef.current > speed) {
      dispatch(moveDown())
      progressTimeRef.current = 0
    }
    lastUpdateTimeRef.current = time
  }
  ... 
```

The function `update` takes `time` as a parameter. It calls `requestAnimationFrame` with an argument of `update` itself! Is this recursion? Could be! 

It checks `isRunning`, exiting early if false. You don't want things moving if the game is not running? 

Next, it checks the `lastUpdateTime` if it hasn't been set it sets it to the `time`. Time in this case is the last time since `requestAnimationFrame` was called. 

Next, it calculates the `deltaTime`. The delta time is the difference between now and the last time this function was called. We add the delta time to the current time to track it. When the current time is greater than the `speed` of the game `dispatch` a `moveDown` action and sets the current time to 0. 

Note! The code above is still not active yet. You need to call the `update` function, which will happen in the next step. 

**Challenge**

That's a lot! This would be simpler if not for the way React handles components. Read the code description again and identify the points mentioned in the actual code!

# Start listening for updates with useEffect

With the code above in place, nothing is happening until you call `update`. The trick is that you don't want to call it `update` each time the component renders. Instead, you want to call it only the first time the component renders, and only when `isRunning` changes. 

Crazy I know. But think about it. You want to start `requestAnimationFrame` once and have it call itself after that, remember the recursion mentioned above. Otherwise, you would be adding a new request animation frame each time the component is updated.

When `isRunning` changes you want to cancel the `requestionAnimationFrame` or add start it again. 

Add the following after the last block of code. 

```JS 
export default function Controls() {
  ...
  // Initialize request animation frame and remove it when isRunning changes
  useEffect(() => {
    requestRef.current = requestAnimationFrame(update)
    return () => cancelAnimationFrame(requestRef.current)
  }, [isRunning])

  ...
}
```

At this point, the game should run on its moving blocks down the screen one step per second. Blocks should stack up as they reach the bottom. And, the game should display "Game Over" when the stack reaches the top.

The game is almost complete! 

# Now Commit

```bash
$ git add .
$ git commit -m 'timer created'
$ git push
```

# Implement the Pause Resume button

What if you need to use the bathroom, get a snack, or both? With the timer now running, you might need to pause the game and resume it later.

You've already built the Pause and Resume buttons, but at this point, they don't do anything. Luckily the game state has an `isRunning` property for this purpose!

The button already calls the action, you just need to add some code to the reducer that handles this action. 

Implement the `resume` and `pause` actions in `/src/featuers/gameSlice.js`. 

**Challenge**

Find the pause action. Define the function with `state` as a parameter. In the body of the function set the `isRunning` property on `state` to `false`. Then return `state`. 

**Challenge**

Find the `resume` action. The reducer function should take `state` as a parameter, set `isRunning` on the state to `true` and return `state`.

-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-

Find: 

```JS
...
pause: () => {},
...
```

Update to look like this: 

```js
...
pause: (state) => {
  state.isRunning = false
  return state
},
...
```

Now find: 

```JS
...
resume: () => {},
...
```

Update to: 

```JS
...
resume: () => {},
...
```

With these changes in place, the Play/Pause button in the upper right should pause and resume the game. Nice work! 

# Product So Far

You should now be able to pause/resume the game!

![paused](assets/paused.png)

# Now Commit

```bash
$ git add .
$ git commit -m 'Resume and pause implemented'
$ git push
```
