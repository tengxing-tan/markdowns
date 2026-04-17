# Side Effects in Coding

## What it is

A side effect is any behavior in code beyond returning a value from inputs.

A function has side effects if it changes or depends on state outside its local scope.

## Fast test (10 seconds)

Use this check:

1. Does this code write to something external?
2. Does this code read non-local changing state?
3. Would calling it twice change the world twice?

If any answer is yes, it is effectful.

## Typical side effects

- Writing DB rows
- Calling APIs
- Publishing events/messages
- Writing files
- Logging/analytics
- Updating shared/global state
- Mutating passed objects/arrays
- DOM/UI manipulation
- Reading clock/random/env (effectful dependency)

## Pure vs effectful

Pure function:

- Same input -> same output
- No external reads/writes

Effectful function:

- Reads/writes external state
- Output or behavior can vary by environment/time/order

## When to use this note

Open this note when:

- A bug appears only sometimes
- Tests are flaky or hard to isolate
- Code review asks for better separation of logic and IO
- A function is hard to reason about due to hidden mutation
- You need to decide where to place API/DB/UI work

## Why this matters

- Predictability: fewer order/timing bugs
- Testability: less mocking, clearer assertions
- Safety: avoids duplicate writes, emails, charges, events
- Maintainability: easier refactor of business logic

## Placement rule (practical)

Use this split:

- Core logic layer: mostly pure (compute/decide)
- Edge layer: side effects only (IO/integration)

Keep side effects thin and explicit at boundaries.

## Code smell checklist

- Function both calculates and writes to DB/API
- Hidden mutation of input objects
- Reliance on global mutable values
- Time/random used deep in business logic
- Mixed async orchestration and domain rules in one function

## Refactor playbook

1. Extract pure decision logic first.
2. Pass dependencies in as parameters.
3. Return data/intents from pure logic.
4. Execute IO in one boundary function.
5. Add tests for pure logic before integration tests.

## Small examples

Pure:

```js
function calcTotal(items) {
  return items.reduce((sum, x) => sum + x.price, 0);
}
```

Effectful:

```js
async function checkout(items) {
  const total = items.reduce((sum, x) => sum + x.price, 0);
  await fetch("/orders", {
    method: "POST",
    body: JSON.stringify({ items, total }),
  });
}
```

Safer split:

```js
function buildOrder(items) {
  return {
    items,
    total: items.reduce((sum, x) => sum + x.price, 0),
  };
}

async function submitOrder(order) {
  await fetch("/orders", {
    method: "POST",
    body: JSON.stringify(order),
  });
}
```

## Review question to ask every time

What is the smallest part of this flow that can stay pure, and where is the single explicit boundary for effects?
