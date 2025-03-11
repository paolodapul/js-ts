# What's the difference between using `??` and `||` and what are the possible pitfalls when using these?

The `??` (nullish coalescing) and `||` (logical OR) operators both provide fallback values, but they behave differently in important ways:

## Key Differences

- **`??` (Nullish Coalescing)**: Returns the right-hand value only when the left-hand value is `null` or `undefined`
- **`||` (Logical OR)**: Returns the right-hand value when the left-hand value is any "falsy" value (`false`, `0`, `""`, `null`, `undefined`, `NaN`)

## Examples

```javascript
// Nullish coalescing examples
null ?? "fallback"; // Returns "fallback"
undefined ?? "fallback"; // Returns "fallback"
false ?? "fallback"; // Returns false
0 ?? "fallback"; // Returns 0
"" ?? "fallback"; // Returns ""

// Logical OR examples
null || "fallback"; // Returns "fallback"
undefined || "fallback"; // Returns "fallback"
false || "fallback"; // Returns "fallback"
0 || "fallback"; // Returns "fallback"
"" || "fallback"; // Returns "fallback"
```

## Common Pitfalls

1. **Treating valid falsy values as missing**:
   ```javascript
   const count = userCount || 10; // If userCount is 0, this will use 10 instead!
   ```
2. **Form values**:

   ```javascript
   // With ||, empty strings trigger the default
   const username = formValues.username || "Guest"; // "" becomes "Guest"

   // With ??, empty strings are preserved
   const username = formValues.username ?? "Guest"; // "" stays as ""
   ```

3. **Numeric inputs**:

   ```javascript
   function calculateTax(amount, taxRate) {
     // With ||, taxRate of 0% would become 20%!
     const rate = taxRate || 0.2;

     // With ??, taxRate of 0% is preserved
     const rate = taxRate ?? 0.2;
   }
   ```

4. **Booleans**:

   ```javascript
   const isEnabled = settings.enabled ?? true; // Only defaults if null/undefined
   const isEnabled = settings.enabled || true; // Always true if settings.enabled is false
   ```

5. **Chaining behavior differences**:
   ```javascript
   // These expressions have different evaluation rules
   a ?? b || c  // (a ?? b) || c
   a || b ?? c  // a || (b ?? c)
   ```

Using `??` is generally safer when you only want to provide defaults for missing values while preserving intentional falsy values like `0`, `false`, or empty strings.
