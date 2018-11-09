class: center, middle

# Typescript: Types vs Interfaces


### Author: José Miguel Colella
### Email: <jose.colella@dynatrace.com>
### Github: https://github.com/josecolella

---

# Agenda

1. Background
2. Differences
3. Interfaces vs Types
4. My Thoughts
5. Q&A

---


# Background

* Types - [Advanced Types](https://www.typescriptlang.org/docs/handbook/advanced-types.html)
  > Type aliases create a new name for a type. Type aliases are sometimes similar to interfaces, but can name primitives,
  > unions, tuples, and any other types that you’d otherwise have to write by hand.
  > Aliasing doesn’t actually create a new type - it creates a new name to refer to that type. Aliasing a primitive is not
  > terribly useful, though it can be used as a form of **documentation**.

* Interfaces
  > Describes behavior (contract) that must be followed.

  > Requirements that any object implementing the interface must adhere to
---


# Differences

Type aliases don’t create a new name, meaning that looking at the definition of a method that uses types, returns the object type it represents
while interfaces return the Interface

Types cannot be \***extended***, and typescript documentations mentions using interfaces of types for this reason.

# \#FakeNews

```ts
// Extending types though Union
type Config = { environment: string};
type ApplicationConfig = Config & { apiVersion: string }
```


---

# Interfaces vs Types

- Lint rules that explictly mark as warning the use of interface of types: [interface-over-type-literal](https://palantir.github.io/tslint/rules/interface-over-type-literal/)

- Many threads regarding confusion on when to use types vs interfaces, and whether it is [correct to use interfaces over types](https://github.com/palantir/tslint/issues/3248)

---

# My thoughts

- Use interfaces when you are trying to declare behavior


```ts
interface ICacheService {
  set<T>(key: string, value: T): string;
  get<T>(key: string): T
}
```
- Use types when declaring structures

```ts
type ApplicationCheck = {
  upTimeMillis: number;
  apiVersion: number;
  environment: string;
}
type BuildCheck = {
  author: string;
  buildDate: string;
  gitCommit: string;
}
type HealthCheck = ApplicationCheck & BuildCheck;

```

---

class: center, middle

# Q&A
