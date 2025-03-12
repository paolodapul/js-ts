# Private Class Fields

In TypeScript, the hashtag symbol (`#`) is used to designate private class fields and methods. This is part of the ECMAScript private fields feature that TypeScript adopted, and it provides true privacy at runtime, not just during compilation.

Here's what the `#` symbol does:

1. **Creates private class members**: Fields or methods prefixed with `#` are only accessible within the class body.

2. **Enforces privacy at runtime**: Unlike TypeScript's `private` modifier which is only enforced during compilation, `#` private fields remain private at runtime.

3. **Prevents name collisions**: Private fields with `#` won't conflict with public fields of the same name.

Here's an example:

```typescript
class Person {
  #name: string; // Private field
  #age: number; // Private field

  constructor(name: string, age: number) {
    this.#name = name;
    this.#age = age;
  }

  #calculateBirthYear(): number {
    // Private method
    const currentYear = new Date().getFullYear();
    return currentYear - this.#age;
  }

  getInfo(): string {
    return `${this.#name} was born in ${this.#calculateBirthYear()}`;
  }
}

const person = new Person("Alice", 30);
console.log(person.getInfo()); // Works fine

// These would cause errors:
// console.log(person.#name);  // Error: Property '#name' is not accessible outside class 'Person'
// person.#calculateBirthYear();  // Error: Property '#calculateBirthYear' is not accessible outside class 'Person'
```

This is different from TypeScript's `private` keyword, which is a compile-time-only check:

```typescript
class PersonWithPrivate {
  private name: string; // TypeScript private modifier

  constructor(name: string) {
    this.name = name;
  }
}
```

The key difference is that JavaScript runtime actually enforces the privacy of `#` fields, whereas the `private` keyword is only enforced by the TypeScript compiler.
