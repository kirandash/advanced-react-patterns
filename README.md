# Advanced React Patterns

## Helpful Links

### 🖥 [The demo site](https://advanced-react-patterns-ultrasimplified.netlify.com/)

* The development DEMO site lives here: https://dev-advanced-react-patterns-ultrasimplified.netlify.com/

## How do I run the demos locally?

1. Clone this repo

2. Change directory

```sh
cd showcase
```

3. Install dependencies

```sh
npm install
```

or

```sh
yarn install
```

4. Run the app

```sh
npm dev
```

or

```sh
yarn dev
```

## The Patterns implemented

### 1. The Medium Clap

- Initial implementation with class component (src/patterns/01.js)
- Refactor to custom hooks ((src/patterns/02.js))

### 2. Compound Components

- Initial implementation
- With Callback

### 3. Reusable Styles

### 4. Control Props

### 5. Custom Hooks

### 6. Props Collection

### 7. Prop Getters

### 8. State Initializers

### 9. State Reducers

- Initial refactor to useReducer
- With user defined reducer
- With type and reducer export


# Advanced React Patterns - NOTES

## 1. Intro
### 1.1 Why Advanced React Patterns
- **Design Patterns?**
    - Time tested solutions to recurring design problems
    - Christopher Alexander - a british architect came up with the idea of design patterns
    - Software Engineering got inspired from CA

### 1.2 Design Patterns and React
- Reusability
- Easy API
- Style extensibility
- **Advanced React Patterns**:
    - Solve issues related to building reusable components using proven solutions
    - Development of highly cohesive components with minimal coupling
    - Better way to share logic b/w components

### 1.3 [Medium clap component](https://www.freecodecamp.org/news/how-i-re-built-the-medium-clap-effect-and-what-i-got-out-of-the-experiment-991672995fdf/)

## 2. The medium clap real world component for studying advanced React Patterns

## 3. Custom Hooks
### 3.1 Custom Hooks and refs, useCallbacks
- Accessing DOM elements while using reusable components
    - DOM elements can be accessed using id or class selector. But it is alright when using HOC with classes. since they have single instance. But while using hooks or fns, the elements are on global window. So we will have to use unique class names viz: 'kiran-123' or even better use: **refs**.
- **[refs](https://reactjs.org/docs/refs-and-the-dom.html)**:
    - Refs provide a way to access DOM nodes or React elements created in the render method.
    - when to use ref:
        - Managing focus, text selection, or media playback.
        - Triggering imperative animations.
        - Integrating with third-party DOM libraries.
    - refs can be used in two ways:
        - createRef()
        - callback refs (recommended when we have multiple elements to be referenced: since instead of passing individual ref reference we can just pass one fn to all elements)
- **useCallback**:
    - a fn in render method will be called every time component re-renders. But if the fn doesn't need to be computed with every re-render: use useCallback
    - Returns a memoized callback.
    - [Docs](https://reactjs.org/docs/hooks-reference.html#usecallback)

### 3.2 when is my hook invoked and useLayoutEffect
- useClapAnimation ---> useEffect (not called) ---> render() ---> useEffect (called) ---> setRef ---> render() ---> useEffect (not called since no dependency)
- elements are defined only in setRef. So must do an undefined check in useEffect for elements
- **useLayoutEffect**
    - for DOM related changes: instead of using useEffect, use **useLayoutEffect**
    - for smoother and buttery animations
    - [Docs](https://reactjs.org/docs/hooks-reference.html#uselayouteffect)
    - The signature is identical to useEffect, but it fires synchronously after all DOM mutations. Use this to read layout from the DOM and synchronously re-render. Updates scheduled inside useLayoutEffect will be flushed synchronously, before the browser has a chance to paint.
    - usage: DOM animations etc
