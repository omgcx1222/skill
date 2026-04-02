---
name: react
description: Use this skill when generating or modifying React code.
---

# Core Principles

- Mmust this stack unless explicitly instructed otherwise.
- Prefer simplicity over abstraction, Avoid unnecessary complexity.
- For the naming of variables and overly complex logic, Chinese comments must be added.
- Unless otherwise specified, do not remove the console from the original code.
- Avoid using multi-level relative paths and use path aliases instead.

---

# Hook Rules

Consider using React hooks in the following scenarios:

- Rendering large lists
- Frequent state updates
- Sub-components re-rendering due to changes in object references

## For simple event handlers, inline functions are allowed.

- the logic is trivial
- the component is not performance critical
- the handler is not passed deeply to memoized children

Example:

```tsx
<Button onClick={() => setOpen(true)} />
```

## When logic grows slightly, extract it into a local function.

Example:

```tsx
const handleOpen = () => {
  // todo
}

;<Button onClick={handleOpen} />
```

## Should use `useCallback` only when **reference stability matters**.

- function passed to components
- function used inside dependency arrays
- functions capturing many variables
- components rendered frequently in large lists

Example:

```tsx
const handleOpen = useCallback(() => {
  // todo
}, [])
```

## useMemo

Should use `useMemo` when:

- performing expensive calculations
- deriving complex objects or arrays
- preventing unnecessary re-renders due to new references

Example:

```tsx
const filteredUsers = useMemo(() => {
  return users.filter((user) => user.active)
}, [users])
```

---

# Component Rules

Should design React components following three principles:

- Repeat → Reusable Component. avoid repetition.
- Layout → UI Component. keep UI structure consistent
- Complex Logic → Child Component. isolate complex logic

---

## General Guidelines

- Components should have a **single responsibility**
- Avoid very large components
- Prefer clear component names
- Prefer composition over deeply nested JSX

## Component Invocation

React components must be used with **JSX syntax**, not as normal function calls.

Bad:

```tsx
UserCard({ user })
```

Good:

```tsx
<UserCard user={user} />
```
