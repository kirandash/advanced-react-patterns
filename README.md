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

## 2. The medium clap real world component for studying advanced React Patterns - with **HOC Pattern**
- Code (patterns/01.js)

## 3. Custom Hooks Pattern
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

## 4 Compound Components Pattern
### 4.1 Understanding CC (src/03.js)
- Exposing both main and children components to user instead of exposing a large lump viz partent component
    - Ex: MediumClap component is a large component that we are exposing
    - Implementing the compound components pattern we will expose MediumClap and also the ClapIcon, CountTotal, ClapCount components.

### 4.2 Why Compound Components
- **Benefits**:
    - Customizability
    - Understandable API: easily readable
    - Props overload
        - If we expose only the parent component: all props for children has to be passed through parent.
        - If we expose the child component: we can send props to the right child component

### 4.3 How to implement the pattern
- All the driving logic will be passed in to parent component (MediumClap)
    - MediumClap: locomotive
        - ClapIcon, CountTotal, ClapCount: carriages or context object

### 4.4 Refactor to compound components
- Use context object to share data b/w main and child components
    - [Docs](https://reactjs.org/docs/context.html)
- Provider: contains values for child component in context obj
- useMemo: to pass props to Provider
    - not pass props directly as object
    - since if outer component changes: provider will re-render and pass props again
    - useMemo so that calculation doesn't happen every time
- For child components: Instead of getting data from props, get it from context

### 4.5 Alternative export strategy
- Method 1: `import MediumClap, { ClapIcon, ClapCount, CountTotal } from 'medium-clap'`
    - Have to import parent and child components separately
- Method 2: `import MediumClap from 'medium-clap'`
    - Use: `MediumClap.Icon`
- Both methods are equally valid

### 4.6 Exposing state via a callback
- Add callback onClap to MediumClap
    - trigger callback using useEffect every time count changes
    - the callback will also occur on componentDidMount

### 4.7 Invoking the useEffect callback only after mount
- using useRef hook

## 5. Patterns for crafting reusable styles
### 5.1 Intro to reusable styles
- We must allow user to be able to change styles of our reusable component
- can overwrite styles in 2 ways:
    - inline style
    - class name

### 5.2 Extending styles via a style prop (src/patterns/04.js)
- Allowing user to be able to style any of the child components
    - MediumClap.Icon, MediumClap.Count and MediumClap.Total
- Inline styles are not cool

### 5.3 Extending styles via a className prop
- extending style with class name
- `className={userStyles.icon}`
- combining class names: 
    - combining multiple class names - our class name and users class names
    - using array to combine classes is much cleaner than using ${} string concatenation

## 6 The control Props pattern (src/patterns/05.js)

### 6.1 Problem to be solved
- Allowing user to control component's internal props
    - count, countTotal, isClicked

### 6.2 What is control props
- concept similar to controlled inputs: (inputs controlled with value and onChange event)
- **controlled props**: we will make MediumClap a controlled component so user can pass callback and value to it
- `<MediumClap values={} onClap={} />`

### 6.3 Implementing the pattern

### 6.4 Practical usage

