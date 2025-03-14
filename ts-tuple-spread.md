# TypeScript Tuple Spread Operator

```typescript
type Foo<T extends any[]> = [boolean, ...T, boolean];
```

The `...T` in `[boolean, ...T, boolean]` uses TypeScript's **tuple type spread operator**, which works differently from JavaScript's spread operator. While they look similar, they serve different purposes.

### How It Works

- **Type-Level Spread**:  
  This happens purely in TypeScript’s type system at compile time.  
  It allows you to insert all elements from a tuple type (`T`) into another tuple type at any position.
- **Tuple Types Are Fixed-Length Arrays**:  
  Tuples in TypeScript are arrays with known lengths and element types at specific positions.

- **Special Syntax for Tuple Composition**:  
  TypeScript added tuple spreads at the type level to enable flexible composition and transformation of tuple types.

### Practical Example

```typescript
type PaymentInfo = [string, number]; // [paymentId, amount]
type Foo<T extends any[]> = [boolean, ...T, boolean];

type PaymentEnvelope = Foo<PaymentInfo>;
// Result: [boolean, string, number, boolean]

const payment: PaymentEnvelope = [true, "payment-123", 99.99, false];
//                                 ^      ^            ^      ^
//                              isValid  paymentId   amount  isProcessed
```

```typescript
type PaymentDetails = [string, number, string];
type IPaymentRequest<T extends any[]> = [boolean, ...T, boolean];
type StandardPaymentRequest = IPaymentRequest<PaymentDetails>;

const request: StandardPaymentRequest = [
  true,
  "merchant-123",
  99.99,
  "USD",
  true,
];
```

### Comparison to JavaScript Spread

At **runtime**, JavaScript's spread operator (`...`) spreads **values** into arrays, and it can be used in the middle of array literals:

```javascript
const someArray = ["payment-123", 99.99];
const payment = [true, ...someArray, false];
```

However, JavaScript doesn’t enforce the shape or length of arrays. TypeScript’s tuple spreads happen at the **type level**, enforcing structure, length, and type safety.

### Why This Is Useful

Tuple spreads are especially valuable in domains like **payments** or **messaging systems**, where you need consistent, type-safe message formats that wrap varying payload types.
