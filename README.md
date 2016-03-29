# Redux

### First Principle

Represent the whole state of your app as a single javascript object

All mutations and changes to the state are explicit, so it is possible to keep track of all of them

“Everything that changes in your app including the data and the UI state is included in a single object, we call the state or the state tree.” 


### Second Principle

The state tree is *read only*, you can not modify or write to it

The only way to change the state tree is by *dispatching and action*, an action is a plain javascript object

An action is the minimal representation of the change to that data

Only requirement is that it has a type property (use strings because they are serializable) 


### Note on Pure and Impure Functions

Pure Functions..

a) are the functions whose return value depends solely on the values of their arguments. 

b) do not have any observable side effects, such as network or database calls

c) predictable

d) do not modify values passed to them

*Pure functions have two very nice properties. They are easy to think about, and they are easy to re-use.* - [Eloquent Javascript]

### Third Principle

To describe state mutations you have to write a function that takes the previous state of the app, the action being dispatched and returns the next state of the app - and this function has to be pure. this function is called the `reducer`

The UI is most predictable when it’s described as a pure function of the application state


### Example App from [Redux]

```js
import { createStore } from 'redux'

/**
 * This is a reducer, a pure function with (state, action) => state signature.
 * It describes how an action transforms the state into the next state.
 *
 * The shape of the state is up to you: it can be a primitive, an array, an object,
 * or even an Immutable.js data structure. The only important part is that you should
 * not mutate the state object, but return a new object if the state changes.
 *
 * In this example, we use a `switch` statement and strings, but you can use a helper that
 * follows a different convention (such as function maps) if it makes sense for your
 * project.
 */
function counter(state = 0, action) {
  switch (action.type) {
  case 'INCREMENT':
    return state + 1
  case 'DECREMENT':
    return state - 1
  default:
    return state
  }
}

// Create a Redux store holding the state of your app.
// Its API is { subscribe, dispatch, getState }.
let store = createStore(counter)

// You can subscribe to the updates manually, or use bindings to your view layer.
store.subscribe(() =>
  console.log(store.getState())
)

// The only way to mutate the internal state is to dispatch an action.
// The actions can be serialized, logged or stored and later replayed.
store.dispatch({ type: 'INCREMENT' })
// 1
store.dispatch({ type: 'INCREMENT' })
// 2
store.dispatch({ type: 'DECREMENT' })
// 1
```


[Redux]: <https://github.com/reactjs/redux>
[Eloquent Javascript]: <http://eloquentjavascript.net/1st_edition/chapter3.html>