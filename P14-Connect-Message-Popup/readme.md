
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
1. **Connect each component up to state and reducers**
    1. ~~NextBlock~~
    1. ~~GridBoard~~
    1. ~~Controls~~
    1. **Message-Popup**
        1. **Implement the `mapStateToProps` function**
        1. **Implement the `mapDispatchToProps` function**
        1. **Connect the `message-popup` component**
        1. **Update the `render` method to display the appropriate text based on the state of the game**
1. Implement block rotation
1. Implement moving blocks
1. Building a timer system
1. Implementing Game Over and Restart

Time for the message popup to connect to `state`! This will allow you to show the message popup when the game changes state, such as when the game is paused or ends.

The message popup should display when the game is paused or over. Otherwise it will be invisible. _Remember we're using CSS to control the position and visibility._

Currently the popup displays all the time. You can fix this in two steps:

1. Retrieve the `isRunning` and `gameOver` properties from `state`
1. Use them to display or hide the popup by adding or removing a CSS class name to the component's parent element!

# Hide and show the MessagePopup

This is an opportunity to see where Redux is really helping you manage your application state. The MessagePopup component is can easily be displayed or hidden based on state without having to do much work or without tightly coupling it to the rest of the application. 

Use the following logic to hide and show the message popup.

- If `isRunning` and `gameOver` is `false` the message popup
should be hidden. Hide it by adding the `hidden` class to
`className`.
- If `isRunning` is `false` the message popup should be visible
and the message text should say 'Paused'.
- If `gameOver` is `true` the message popup should be visible
and the message text should say 'Game Over'.

Again, try this on your own, and then check against the solution to see how well you matched up.

> [solution]
>
> Updated `render` method in `/src/components/message-popup.js`:

```js
import React from 'react'
import { useSelector } from 'react-redux'

// Displays a message
export default function MessagePopup(props) {
  const isRunning = useSelector((state) => state.game.isRunning)
  const gameOver = useSelector((state) => state.game.gameOver)

  let message = ''
  let isHidden = 'hidden'

  if (gameOver) {
    message = 'Game Over'
    isHidden = ''
  } else if (!isRunning) {
    message = 'Paused'
    isHidden = ''
  }

  return (
    <div className={`message-popup ${isHidden}`}>
      <h1>{message}</h1>
    </div>
  )
}
```

# Product So Far

Refresh the browser to see the popup should now be hidden! Our Message Popup now **uses Redux/Flux to manage application state!**

![hidden-popup](assets/hidden-popup.png)

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'Added connection for message popup'
$ git push
```
