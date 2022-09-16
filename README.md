# Learning_React
 Using the Create-React-App tutorial to learn React

2022/08/29
9:04am - 11:45am

-I will be using the React website tutorial (https://reactjs.org/docs/create-a-new-react-app.html) to 
 begin learning how to create React SPA's
-First step is to use NPX to initialize the app, requires Node >= 14.0 and NPM >= 5.6, will confirm 
 these versions first.
 -Node is not yet installed, will install now.
 -installed Node Version Managager (https://gist.github.com/d2s/372b5943bce17b964a79) and currently 
  using NodeJs version 16.15.1
 -Used comman npm create-react-app (Package needed to be installed first) to create the app 
  learn-react
 -Ran app with npm start to confirm it worked, it did
-Tutorial states, when ready for deployment, run npm run build to creat build envrionment
-React works with NextJs framework for styling and routing, a tutorial is provided that I will
 check out later, for now will continue with this one.

-Tutorial Application is a tic tac toe game, first step is to remove all file WITHIN the src folder
-Next is to create the index.css file which will contain all styles, and index.js to contain the
 JavaScript code
-Need to import React and ReactDOM modules at top of index.js files as well as the newly created
 css file
-running npm start should now show an empty tic tac toe board....confirmed
-updated square component to render value property within the button(this.props.value)
-updated board component to return the (i) value of the square button
 -this is a demonstration of how to pass property values between React components.
-added click function to square button which logs "click" to the console
-To have the component remember it was clicked, we use state by adding a constructor to the Square
 component with props as an element, and setting this.state object with a property: value, set to null
 super(props) needs to be called when defining a subclass constuctor
-Changing the Square components render() method to display an "X" when clicked(the states current
 value) with setState in the onClick method, this will re-render the square whenever it is clicked
-Tested app to make sure when a square is clicked an X appears and it did
-Added React Developer Tools add-on to Firefox to inspect component tree
-Next step is to store square property values in the parent Board component to keep track of state
 known as Lifting State, Board component will contain an square array with 9 null values
-Now I have to use the property passing method to determine if a square is either: 'null','X', or 'O'
 by updating the renderSquare function to return value = {this.state.squares[i]} and adding an onCLick
 function to handle the click event
-Since Board will be handling the state, I can delete the constructor from the Square component
-The handleClick() function will be added to the Board class to handle what happens when a square is
 clicked
-Square class component can be replaced with a function component that returns the square button with
 it's properties
-Next, turn functionality will be implemented to allow player 'O' to have a turn:
 -first I have to update the state of the Board component to have a property to set player 'X' to
  default, xIsNext: true
 -within the handleClick() function create a squares property that contains logic value for which 
  player is active and update the setState property to change xIsNext to false
 -change status of which players turn it is by using the squares[i] property in the handleClick()
  function
-Running app to make sure functionality is working...functions properly, next is to add Winning logic
-calculateWinner function will be added to end of js file. It contains an array of winning line arrays
 and a for loop to itterate through winning arrays
-Next will be updating the Board components render() function to display if a winner is found

2022/09/16
8:30AM

-winner variable will call calculateWinner function with the squares state, update the status based on
 who is next or if a player wins.
-update to Board components handleClick function will ignore a click if there is a winner or if a 
 square has already been clicked
-game is technically complete at this point, further exercise will add in time travel functionality
 to go back to previous moves
-having an issue with app loading a blank page when running npm start
 -issue was when calling calculateWinner function, I called the winner state rather than the squares
  state, found issue by looking through developer console errors
-history array will be contained in Game component to go back to previous moves
 -constructor is added and state is defined with history array
-constructor in Board component will be deleted and squares and onClick props will be recieved from 
 Game component, this.state.squares[i] is replaced with this.props.squares[i] and this.handleClick()
 is replaced with this.props.onClick() in renderSquare function
-Game components render function will be updated to display recent history to determine game status
-Board component handleClick method is moved to Game component and modified to update history display
 -concat method is used on history array to prevent mutation of original array
-moves variable will map history array to allow player to go back to certain moves or go back to start
 of game, moves will be output in an ordered list in the Game components return method.
-had an issue where squares was undefined, forgot to update calculateWinner in Game components render
 function to use current rather than this.state