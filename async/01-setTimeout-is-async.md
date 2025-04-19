### setTimeout is asynchronous

`setTimeout` is one of the core asynchronous operations in JavaScript, allowing you to schedule code execution after a specified delay without blocking the main thread.

When you call `setTimeout`, it registers the callback function to be executed later and immediately returns, allowing the rest of your code to continue executing.

After the specified delay, the callback function is placed in the event queue, and will be executed when the call stack is empty.

### Example

```typescript
console.log("Start");

setTimeout(() => {
  console.log("Timeout callback executed");
}, 1000);

console.log("End");

// What if I want the operation that took 1 second to complete
// To finish before executing the rest of the code
// AND without blocking the event loop?
//
// Options:
// Callbacks -> Promise Chaining -> Async/await
```

```typescript
// Callback
console.log("starting");

setTimeout(() => {
  console.log("after waiting 1 second");

  // Next operation happens here, in the callback
  doNextThing();
}, 1000);

function doNextThing() {
  console.log("Next operation completed");
}
```

```typescript
// Promise chaining
function delay(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms));
}

console.log("Starting");

delay(1000)
  .then(() => {
    console.log("After waiting 1 second");
    return "Next operation";
  })
  .then((result) => {
    console.log(result);
    console.log("All done");
  });
```

```typescript
// Async-await (feat. top-level await)
async function myFunction() {
  console.log("Starting");

  // Convert setTimeout to a Promise
  await new Promise((resolve) => setTimeout(resolve, 1000));

  console.log("After waiting 1 second");

  // Continue with code that depends on the timeout completing
  return "Done";
}

const res = await myFunction();
console.log(res);
```
