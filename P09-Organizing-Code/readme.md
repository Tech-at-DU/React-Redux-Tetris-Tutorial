# Organizing Code

1. ~~Implement the overall grid square~~
1. ~~Implement the game board~~
1. ~~Implement the "next block" area~~
1. ~~Implement the score board~~
1. ~~Arrange the layout of the game~~
1. ~~Implement the controls~~
1. ~~Implement the message popup~~
1. ~~Implement the actions and reducers~~
1. **Do some code organizing and cleanup**
    1. **Create utils to cover ancillary functions**
1. Implement state and shapes
1. Connect each component up to state and reducers
1. Implement block rotation
1. Implement moving blocks
1. Building a timer system
1. Implementing Game Over and Restart

Keeping files organized is important. Rather than clutter components with more code, it's a good idea to move code to other modules and import it where needed.

# Overview of the code

Let's get a sense of the structure of our game:

- The game will manage the game board as an array.
- Each of the blocks will also be defined as an array
- Each shape will be defined as one or more arrays representing the rotation of a block.

This is a lot of arrays that need to be defined.

Rather than clutter a component or reducer with all of these the goal will be to make _another file_ that contains functions and variables that are used by components.

# Utils

The game needs to generate random numbers. The `Math.random()` works but we will need to get integers in a range. It will be good to define a function that is easier to work with.

Add a new file `/src/utils/index.js` with the following function in it:

**Challenge**

Write a function that takes in a min and max value and returns a number in this range inclusive. 

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

Does your solution look simial to this? 

```JavaScript
export const random = (min, max) => {
  return Math.floor(Math.random() * (max - min + 1)) + min
}
```

The function above taks in a min value and max value, two numbers, and returns a random number in that range. 

As the project progresses any time we need more general purpose code we can add it to this file, export, and import as needed.

# Now Commit

```bash
$ git add .
$ git commit -m 'Added utils'
$ git push
```
