# test-lifecycle-methods

## What are React lifecycle methods?

`You can think of React lifecycle methods as the series of events 
that happen from the birth of a React component to its death.`

Every component in React goes through a lifecycle of events. 
I like to think of them as going through a cycle of birth, growth, and death.

**Mounting** - Birth of your component  
**Update** - Growth of your component  
**Unmount** - Death of your component  
      
Now that we understand the series of lifecycle events let’s learn more about how they work.

## React Lifecycle Methods

### render()

The _render()_ method is the most used lifecycle method. You will see it in all React classes. 
This is because _render()_ is the only required method within a class component in React.

As the name suggests it handles the rendering of your component to the UI. 
It happens during the **mounting** and **updating** of your component.

Below is an example of a simple render() in React.

