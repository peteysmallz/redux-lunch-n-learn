# Redux

### First Principle

Represent the whole state of your app as a single javascript object

All mutations and changes to the state are explicit, so it is possible to keep track of all of them

“Everything that changes in your app including the data and the UI state is included in a single object, we call the state or the state tree.” 


### Second Principle

The state tree is read only, you can not modify or write to it

the only way to change the state tree is by dispatching and action, an action is a plain javascript object

Instead anytime you want to change the state, you need to dispatch an action 

an action is a plain javascript object describing the change

- the action is the minimal representation of the change to that data

only requirement is that it has a type property (use strings b/c serializable) 


### Note on Pure and Impure Functions

Pure Functions..

a) are the functions whose return value depends solely on the values of their arguments. 

b) do not have any observable side effects, such as network or database calls

c) predictable

d) do not modify values passed to them


### Third Principle

To describe state mutations you have to write a function that takes the previous state of the app, the action being dispatched and returns the next state of the app - and this function has to be pure. this function is called the `reducer`

The UI is most predictable when it’s described as a pure function of the application state