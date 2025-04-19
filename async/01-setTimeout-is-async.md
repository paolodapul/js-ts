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
