# test-lifecycle-methods

## What are React lifecycle methods?

`You can think of React lifecycle methods as the series of events that happen from the birth of a React component to its death.`

Every component in React goes through a lifecycle of events. 
I like to think of them as going through a cycle of birth, growth, and death.

***Mounting*** - Birth of your component   
***Update*** - Growth of your component  
***Unmount*** - Death of your component  
      
Now that we understand the series of lifecycle events let’s learn more about how they work.

## React Lifecycle Methods

### render()

The _render()_ method is the most used lifecycle method. You will see it in all React classes. This is because _render()_ is the only required method within a class component in React.

As the name suggests it handles the rendering of your component to the UI. It happens during the **mounting** and **updating** of your component.

_render()_ method returns JSX that is displayed in the UI. A render() can also return a null if there is nothing to render for that component.

**A _render()_ method has to be pure with no side-effects.**

React requires that your _render()_ is pure. Pure functions are those that do not have any side-effects and will always return the same output when the same inputs are passed. This means that you can not _setState()_ within a _render()_ .

`You cannot modify the component state within the _render()_.`

If you do need to modify state that would have to happen in the other lifecycle methods, therefore keeping _render()_ pure.

Furthermore, keeping your _render()_ simple and clean without state updates makes your app maintainable.

### componentDidMount()

Now your component has been mounted and ready, that’s when the next React lifecycle method ***_componentDidMount()_*** comes in play.

_componentDidMount()_ is called as soon as the component is mounted and ready. This is a good place to initiate API calls, if you need to load data from a remote endpoint.

Unlike the _render()_ method, _componentDidMount()_ allows the use of _setState()_. Calling the _setState()_ here will update state and cause another rendering but it will happen before the browser updates the UI. This is to ensure that the user will not see any UI updates with the double rendering.

`You can modify the component state within the _componentDidMount()_ , but use it with caution.`

**Caution:** It is recommended that you use this pattern with caution since it could lead to performance issues. The best practice is to ensure that your states are assigned in the _constructor()_. The reason React allows the _setState()_ within this lifecycle method is for special cases like tooltips, modals, and similar concepts when you would need to measure a DOM node before rendering something that depends on its position.

### componentDidUpdate()

This lifecycle method is invoked as soon as the updating happens. The most common use case for the _componentDidUpdate()_ method is updating the DOM in response to prop or state changes.

You can call _setState()_ in this lifecycle, but keep in mind that you will need to wrap it in a condition to check for state or prop changes from previous state. Incorrect usage of _setState()_ can lead to an infinite loop.

`You can modify the component state within the _componentDidUpdate()_ , but use it with caution.`

Take a look at the example below that shows a typical usage example of this lifecycle method.

`componentDidUpdate(prevProps) {<br /> 
      //Typical usage, don't forget to compare the props<br/> 
      if (this.props.userName !== prevProps.userName) {  
            this.fetchData(this.props.userName);  
      }  
}`  

Notice in the above example that we are comparing the current props to the previous props. This is to check if there has been a change in props from what it currently is. In this case, there won’t be a need to make the API call if the props did not change.

### componentWillUnmount()

As the name suggests this lifecycle method is called just before the component is unmounted and destroyed. If there are any cleanup actions that you would need to do, this would be the right spot.

`You cannot modify the component state in componentWillUnmount lifecycle.`

This component will never be re-rendered and because of that we cannot call _setState()_ during this lifecycle method.

Common cleanup activities performed in this method include, clearing timers, cancelling api calls, or clearing any caches in storage.

### shouldComponentUpdate()

This lifecycle can be handy sometimes when you don’t want React to render your state or prop changes.

Anytime _setState()_ is called, the component re-renders by default. The _shouldComponentUpdate()_ method is used to let React know if a component is not affected by the state and prop changes.

Keep in mind that this lifecycle method should be sparingly used, and it exists only for certain performance optimizations. You cannot update component state in _shouldComponentUpdate()_ lifecycle.

**Caution:** Most importantly, do not always rely on it to prevent rendering of your component, since it can lead to several bugs.

`shouldComponentUpdate(nextProps, nextState) {  
      return this.props.title !== nextProps.title ||   
            this.state.input !== nextState.input   
}`  

As shown in the example above, this lifecycle should always return a boolean value to the question, **_“Should I re-render my component?”_**
