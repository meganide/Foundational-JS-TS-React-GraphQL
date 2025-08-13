# Typescript

## What is Typescript?
It's a superset of Javascript that adds static typing and modern langauge features. It compiles down to plain Javascript, so it can run anywhere Javascript runs.

**Differences**
- Typescript has optional static types
- includes features like interfaces, enums, generics
- Requires compilation before running
- Offers better tooling support (autocomplete, type checking)

## Benefits
- Early detection of errors during compile time
- Better developer experience (intellisense, autocomplete)
- Easier refactoring and maintainability
- Enforces contracts between components

## Type inference
Typescript automatically infers the type of a variable from its initial values without needing explicit annotation.

## Diff between `any`, `unknown`, `never`
- `any` --> Opts out of type checking entirely
- `unknown` --> Similair to `any`, but must be type-checked before usage
- `never` --> Represents values that never occur (a function that throws or infinite loop)

## Type alias vs interface
- **Interface:** Primarily for object shapes and can be exended/merged
- **Type alias:** Can represent any type (primitive, union, intersection)

## Union and intersection types
- **Union ( | ):** A value that can be of multiple types
- **Intersection ( & ):** A value must satisfy multiple types at once

## Void
The void type represents the unavailability of the data type for any variable. Used for functions that return nothing.

## Literal types
A type that represent a specific value

```ts
type Direction = "up" | "down" | "left" | "right";
type DiceRoll = 1 | 2 | 3 | 4 | 5 | 6 | 7
```

## Type narrowing
Refining a variables type based on checks.

```ts
function printId(id: string | number) {
  if (typeof id === "string") {
    console.log(id.toUpperCase());
  }
}
```

## Function overload
Multiple function signatures for the same implementation

```ts
function example(x: number): number;
function example(x: string): string;
function example(x: any): any {
  return x;
}
```

## Generics
Generics let you write reusable components that work with any type.

```ts
function identity<T>(value: T): T {
  return value;
}
```

You can constrain a generic type parameter with the extends keyword.

```ts
function logLength<T extends { length: number }>(item: T) {
  console.log(item.length);
}
```

## `keyof`, `typeof`, `in`
- `keyof` -> gets all keys of a type
- `typeof` -> gets the type of a variable or object
- `in` -> iterates over keys in mapped types