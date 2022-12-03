---
title: "Creating a Timer"
slug: creating-a-timer
---

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
    1. **Build out an `update` function to update the GridBoard as blocks fall down**
    1. **Implement the logic in the Pause/Resume button**
1. Implementing Game Over and Restart

With what we have so far, the game is almost finished. One important step is needed to make turn this into a playable game: the blocks need to move down on their own!

To make this work the game needs to issue `MOVE_DOWN` actions on it's own. The time between each of these actions will determine the difficulty.

You're going to use `requestAnimationFrame` to implement this feature. It may seem a little strange, but it has a couple advantages over using something like `setInterval`, and is a great way to practice some new ideas.

# Dispatching a periodic MOVE_DOWN action

The goal here is issue a MOVE_DOWN action every time period, where the time period might start at once per second and decrease over time as the game is played to increase difficulty.

> [info]
>
> You're going to be referring to **Delta time** a lot in this chapter. Delta time represents the difference between now and the last time the browser redrew the window.

As usual, let's go over some basic requirements:

- The game needs to handle time and issue MOVE_DOWN
actions at intervals.
- The interval will be the speed set on state.
- Timing should be handled in the GameBoard component

> [info]
>
> You could place the timing code in the App or Controls or other Component as well

# Request Animation Frame Overview

The browser draws the contents of the window at regular intervals, about every 16.7 milliseconds. It's advantageous to our application to update our views on the same clock.

JavaScript provides a method to notify our applications when the browser is about to redraw the screen.

[requestAnimationFrame()](https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame) is a method that takes a callback that is executed just before the browser redraws the window.

# useRef()

When components are created from components values that are used by the component would be lost by the time the component finishes rendering. 

There are times you'll need a component to "remember" a value it used the last time it rendered/ran. 

React provides two hooks for this purpose. 

- useState
- useRef

The useState hook let's you define values that when changed will cause the component to render again. 

The useRef hook will hold on to a value value and changing this value won't automatically render the component. 

In the Tetris game you'll be receiving updated every "frame", which is about 30 to 60 times per second, but you'll only be makng changes that need to be rendered about 1 time per second. In this case useRef is the better choice. 

# useEffect

The useEffect hook is used to handle lifecycle events for a component. 

A component is a function as such each time the component is rendered all fo the code in the function is run. In some cases you may have code that should only be run the first a component is added to the DOM, or code that is run when a component removed from the DOM. These are lifecycle events, and useEffect covers these. 

# Making things move

To make things move in the game you'll combine useRef and useEffect. 

The idea is to calculate the time between calls to requestAnimationFrame and when the time is greater than the speed of the game dispatch a move down action. 

this means that you'll be getting requestAnimationFrame updates often but changing state and rendering components less often. 

Import useEffect and useRef. You'll also need useDispatch to update your application state so import that also. 

To move a piece down the screen you'll need a reference to the dispatcher and an action to dispatch. Import these also. 

> [action]
>
> Add the following within the `GridBoard` class in `/src/components/GridBoard.js`:
>
> Update your import statement at the top of the file. 
>
```JS 
import React, { useEffect, useRef } from 'react'
import { useSelector, useDispatch } from 'react-redux'
import { moveDown } from '../actions'
...
```
>

Next define some refs. You'll three. 

- requestRef - Holds a referece to requestAnimationFrame
- lastUpdateTimeRef - tracks the time of the last update
- progressTimeRef - tracks the total time between updates

You also need a reference to the dispatcher since you'll be dispatching a move down action periodically. 

> [action]
>
> Add the following within the `GridBoard` class in `/src/components/GridBoard.js`:
>
> Add the following at the top of the function GridBoard
>
```JS 
export default function GridBoard(props) {
  const requestRef = useRef()
	const lastUpdateTimeRef = useRef(0)
	const progressTimeRef = useRef(0)
  const dispatch = useDispatch()
  ...
}
```
>

# Adding an update function

Write a function that will handle updates from requestAnimationFrame. This function will be defined inside the GridBoard function, after the variables at the top, and before the return statement. 

> [action]
>
> Add the following within the `GridBoard` class in `/src/components/GridBoard.js`:
>
> Add the update function.  
>
```JS 
export default function GridBoard(props) {
	...
>
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
>
  return (
    ...
  )
}
```
>

# Start listening for updates with useEffect

You need to start listening for updates when the component is added to the DOM, and this should only happen once! To prevent the component from running this next block of code on each update you'll wrap in useEffect. 

Add the following after the last block of code. 

> [action]
>
> Add the following within the `GridBoard` class in `/src/components/GridBoard.js`:
>
> Add the following at the top of the function GridBoard
>
```JS 
export default function GridBoard(props) {
  ...
>
  useEffect(() => {
		requestRef.current = requestAnimationFrame(update)
		return () => cancelAnimationFrame(requestRef.current)
	}, [isRunning])
>
  return (
    ...
  )
}
```
>

This should make a game that can be played. Blocks should move down the screen. You may have to wait a moment until they move down into view. A block should stop when it hits the bottom or another block and a new block should start falling. You should be able to move and rotate the blocks. 

There are a couple things that still need to be taken care of. The game doesn't know when it's over. So if blocks stack up a bove the top of the grid it breaks. Also the pause and restart buttons are not wired up yet. 

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'timer created'
$ git push
```

# Implement the Pause Resume button

What if you need to use the bathroom, or get a snack, or both? With the timer now running, you might need to pause the game and resume it later.

You've already built the Pause and Resume buttons, but at this point they don't do anything. Luckily the game state has an `isRunning` property for this purpose!

The button already calls the action, you just need the reducer needs to handle the action.

> [action]
>
> Implement the `RESUME` and `PAUSE` cases in `/src/reducers/game-reducer.js`:
>
```js
case RESUME:
>
      return { ...state, isRunning: true }
>
case PAUSE:
>
      return { ...state, isRunning: false }
```

# Product So Far

You should now be able to pause/resume the game!

![paused](assets/paused.png)

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'Resume and pause implemented'
$ git push
```
