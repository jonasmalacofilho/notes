React
=====

Organize the UI around reusable atoms called components, and state held by React for them.

The UI doesn't modify itself directly; instead, it changes a state variable, and that triggers a new
[Render] of the Component that owns that [State] (and its children).


Component
----------
[Component]: #component

A component is a pure JS function that takes props as a single argument and returns JSX.

```js
function Card({ avatar, name }) { // name must start with uppercase letter
  return ( // JS would parse return\n as return;
  <> <!-- must consist of a single root element (can be a Fragment) -->
    <div className="card-marker"></div>
    <div className="card">
      <Avatar src={avatar} alt={name} /> <!-- must close all tags -->
      <div className="card-name">{name}</div>
    </div>
  </>
  );
}
```

Components maintain state through special hooks: see [State].

[Context] lets a parent component provide data to the entire tree below it. Any component down the
tree that needs to can just read the data from the context with [`useContext`].

**Quirk: hooks like `useState` must only be used at the component top level**.

Components used to be class based, but that has been deprecated.


JSX
---
[JSX]: #jsx

JSX must always be parsed as a single root element.

JSX spread syntax can be used to forward props from one component to another:

```js
function Profile(props) {
    // [ ... ]
    return <Avatar {...props}>;
}
```

but in many cases passing children as JSX might be more appropriate.

To conditionally render a component, one trick is to logical _and_ it with the condition:

```js
<li>{name} {isChecked && "✓"}</li>
```

JSX can be rendered from lists, but each element requires a unique key.

```js
people.map(person => <li key={person.id}>{person}</li>);
```

Keys must be unique among siblings, and must not change.

**Quirk: the short form `<>` Fragment doesn't accept a key; use a `<div>` or the long form
`<Fragment>`.**


State
-----
[State]: #state

Define state with [`useState`]. Avoid redundant or duplicated state variables. The `set` function
returned will update the state _and trigger a re-render._

Don't mutate state directly, only through the `setX` closure returned from `useState`. Generally,
treat state as immutable; but, if necessary, `setX` supports in-place updates by passing in a
closure instead of a (new) value.

State updates are batched within an event handler. All updates and queued until all the code in the
event handler has executed.

Tricks: [Updating Objects in State], [Updating Arrays in State].

Share state by moving it up to the closest common parent, then back down through props.

State is kept by React as long as the corresponding component remains _at the same position in the UI
tree._ A different component at the same position resets the state. To reset state when switching
between instances of the same component, either render them in different positions (tip: an empty
node `{}` still counts as a position), or give each component an explicit `key` identity.

When updating state gets too complex and spread out through various event handlers, this can be
simplified by [Extracting State Logic into a Reducer] ([`useReducer`]). Reducers can be combined
with contexts to manage even more complex state.


Render steps
------------
[Render steps]: #render-steps

([Docs](https://react.dev/learn/render-and-commit))

1. Trigger: on initial render, state change (from events), or parent re-render.

    - While all components should be pure functions, by default a component is always re-rendered if
      their parent re-renders, even if the component props (and state) hasn't changed; to prevent
      this, use [`memo`] (and [`useMemo`]/[`useCallback`]).

2. Render: React calls the component (function) and adds the resulting DOM nodes to its internal UI
   representation (= virtual DOM).

3. Commit: React applies minimal operations to make the DOM match React's internal UI
   representation.

4. Paint: the browser repaints the screen from the DOM.


Escape hatches
--------------
[Escape hatches]: #escape-hatches

[`useRef`] is similar to `useState`, but changes to references don't trigger new renders.

[Effects] allow code to run after rendering, mainly to synchronize with external systems, when
that's not necessary due to a particular event.


Libraries and frameworks
------------------------
[Libraries and frameworks]: #libraries-and-frameworks

[MUI]: a library of based or pre-styled react ui components (mentioned by Caio).

[Tailwind CSS]: a CSS framework that might play well with React.

React-recommended full-stack frameworks support of client-side-only use cases:

- [Next.js]: seems to be "usual" way to do it;
- Gatsby: specifically for static websites, but with a strong focus on GraphQL;
- Remix: very performance-oriented, but doesn't appear to support a "static" use case;


Setup and workflow
------------------
[Setup and workflow]: #setup-and-workflow

Firefox: when working locally, permanently disable HTTP-Only mode for the site, lest the console be
useless.

Extend developer tools with react-devtools (Firefox, Chrome and Edge).


Other
-----

React applications are built from components. Components are built from Hooks, whether built-in or
custom.

Only hooks and components should call other hooks.

Custom hooks must with `use` followed by an uppercase letter.

Strict Mode helps find components that break the rules (only read from props, state and context;
only write to state) by rendering each component twice. To opt into Strict Mode, wrap the root
component into `<React.StringMode>`.

Tutorials:

- [Tutorial: Tic-Tac-Toe (React)](https://react.dev/learn/tutorial-tic-tac-toe)
- [Creating a website with Next.js and React (LogRocket)]
  (https://blog.logrocket.com/creating-website-next-js-react/)
- [Build a real-time chat app with Rust and React (LogRocket)]
  (https://blog.logrocket.com/real-time-chat-app-rust-react/)


<!-- External links -->

[Context]: https://react.dev/learn/passing-data-deeply-with-context
[Effects]: https://react.dev/learn/synchronizing-with-effects
[Extracting State Logic into a Reducer]: https://react.dev/learn/extracting-state-logic-into-a-reducer
[MUI]: https://mui.com/
[Next.js]: https://nextjs.org/
[Tailwind CSS]: https://tailwindcss.com/
[Updating Arrays in State]: https://react.dev/learn/updating-arrays-in-state
[Updating Objects in State]: https://react.dev/learn/updating-objects-in-state
[`memo`]: https://react.dev/reference/react/memory
[`useCallback`]: https://react.dev/reference/react/useCallback
[`useContext`]: https://react.dev/reference/react/useContext
[`useMemo`]: https://react.dev/reference/react/useMemo
[`useReducer`]: https://react.dev/reference/react/useReducer
[`useRef`]: https://react.dev/reference/react/useRef
[`useState`]: https://react.dev/reference/react/useState
