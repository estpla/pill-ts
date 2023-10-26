---
theme: penguin
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## TypeScript: Utility Types
  Gamify Loyalty
drawings:
  persist: false
transition: slide-left
title: TypeScript - Utility Types
colorSchema: dark
layout: intro
---

# TypeScript: Utility Types

Gamify Loyalty

_"Con lo bien que estábamos sólo con JS"_  
_"Como nos la han colao..."_  
_Javi - 2023_

<div class="flex justify-center">
  <img src="/logo.png" class="w-60 h-16 mt-8 shadow" />
</div>

<!--
En esta sesión, exploraremos las Utily Types y los Genericos de TypeScript
-->

---
layout: two-cols
---

# Generics

- Generics make code more flexible.
- Allows working with multiple data types without sacrificing safety.

::right::

```ts
function sort<T>(items: T[]): T[] {
    return items.sort();
}
```

<!--
Genéricos hacen que el código sea más flexible.  
Permite trabajar con múltiples tipos de datos sin sacrificar seguridad.
-->

---
layout: two-cols
---

# Advantages of Generics

- Greater flexibility.
- Safer code.
- Avoids unnecessary duplication.


<!--
Mayor flexibilidad.  
Código más seguro.  
Evita duplicación innecesaria.
-->

---

# Utility Types

- Objects
- Unions
- Functions

<!--
Objetos  
Uniones  
Funciones
-->

---
transition: slide-up
level: 1
---

# Utility Types: Objects

- Partial
- Required
- Omit
- Pick
- Readonly
- Mutable

<!--

-->

---
transition: slide-up
layout: two-cols
level: 2
---

# Partial\<T\>

- Partial\<T\>
- Create a new type that makes all properties of a given type optional.
- Useful when you want to work with partially complete objects.

```ts
type Partial<T> = {
  [P in keyof T]?: T[P];
};
```

::right::

```ts
type User = {
  id: string;
  name: string;
  age: number;
};

type PartialUser = Partial<User>;
```

```ts
type PartialUser = {
  id?: string | undefined;
  name?: string | undefined;
  age?: number | undefined;
};
```

<!--
Partial  
Se utiliza para crear un nuevo tipo que hace que todas las propiedades de un tipo dado sean opcionales.  
Es útil cuando deseas trabajar con objetos parcialmente completos.
-->

---
transition: slide-up
layout: two-cols
level: 2
---

# Required\<T\>

- Required\<T\>
- Makes all properties of a type required, removing their optional status.

```ts
type Required<T> = {
  [P in keyof T]-?: T[P];
};
```

::right::

```ts
type User = {
  id: string;
  name?: string;
  age?: number;
};

type RequiredUser = Required<User>;
```

```ts
type RequiredUser = {
  id: string;
  name: string;
  age: number;
};
```

<!--
Required  
Convierte todas las propiedades de un tipo en propiedades requeridas.
-->

---
transition: slide-up
layout: two-cols
level: 2
---

# Omit\<T, K\>

- Omit\<T, K\>
- Allows to create a new type by excluding specified properties from an existing type.

```ts
type Omit<T, K extends keyof any> = 
  Pick<T, Exclude<keyof T, K>>;
```

::right::

```ts
type User = {
  id: string;
  name: string;
  age: number;
};

type UserWithoutId = Omit<User, "id">;
type UserWithoutMultipleProps = Omit<User, "id" | "name">;
```

```ts
type UserWithoutId = {
  name: string;
  age: number;
};

type UserWithoutMultipleProps = {
  age: number;
};
```

<!--
Omit  
Permite crear un nuevo tipo excluyendo las propiedades especificadas de un tipo existente.
-->

---
transition: slide-up
layout: two-cols
level: 2
---

# Pick\<T, K\>

- Pick\<T, K\>
- Allows to select a subset of properties from a type. 
- Can be use to create a new type that includes only the properties you need.

```ts
type Pick<T, K extends keyof T> = {
  [P in K]: T[P];
};
```

::right::

```ts
type User = {
  id: string;
  name: string;
  age: number;
};

type UserId = Pick<User, "id">;
type UserMultipleProps = Pick<User, "id" | "name">;
```

```ts
type UserId = {
  id: string;
};

type UserMultipleProps = {
  id: string;
  name: string;
};
```

<!--
Pick  
Permite seleccionar un subconjunto de propiedades de un tipo.  
Puedes usarlo para crear un nuevo tipo que incluya solo las propiedades que necesitas.
-->

---
transition: slide-up
layout: two-cols
level: 2
---

# Readonly\<T\>

- Readonly\<T\>
- Turns all properties of a type into read-only properties,
- They cannot be modified after initialization.

```ts
type Readonly<T> = {
  readonly [P in keyof T]: T[P];
};
```

::right::

```ts
type User = {
  id: string;
  name: string;
  age: number;
};

type ReadonlyUser = Readonly<User>;
```

```ts
type ReadonlyUser = {
  readonly id: string;
  readonly name: string;
  readonly age: number;
};
```

<!--
Readonly  
Convierte todas las propiedades de un tipo en propiedades de solo lectura.  
Lo que significa que no se pueden modificar después de la inicialización.
-->

---
transition: slide-up
layout: two-cols
level: 2
---

# Mutable\<T\>

- Mutable\<T\>
- There is no utility type to make a type mutable, but we can create it.

```ts
type Mutable<T> = {
  -readonly [K in keyof T]: T[K];
}
```

::right::

```ts
type User = {
  readonly id: string;
  readonly name: string;
  readonly age: number;
};

type MutableUser = Mutable<User>;
```

```ts
type MutableUser = {
  id: string;
  name: string;
  age: number;
};
```

<!--
Mutable  
Opuesto a Readonly.  
No existe un tipo de utilidad para hacer que un tipo sea mutable, pero podemos crearlo.
-->

---

# Utility Types: Unions

- Union
- Exclude
- Discriminated
- Extract
- NonNullable

<!--

-->

---
transition: slide-up
layout: two-cols
level: 2
---

# Unions

- Allows to combine multiple types into one.
- Useful for handling different input types, optional values, error handling.
- Enhance flexibility and type safety in code.

::right::

```ts
type Role = "admin" | "user" | "anonymous";
```

```ts
type StringOrNumber = string | number;
```

<!--
Unions  
Permite combinar varios tipos en uno.  
Útil para manejar diferentes tipos de entrada, valores opcionales, manejo de errores.  
Mejora la flexibilidad y la seguridad de tipos en el código.
-->

---
transition: slide-up
layout: two-cols
level: 2
---

# Exclude\<T, K\>

- Exclude\<T, K\>
- Create a new type by excluding specific types from another type.

```ts
type Exclude<T, U> = T extends U ? never : T;
```

::right::

```ts
type Role = "admin" | "user" | "anonymous";

type NonAdminRole = Exclude<Role, "admin">;
type UserRole = Exclude<Role, "admin" | "anonymous">;
```

```ts
type NonAdminRole = "user" | "anonymous";

type UserRole = "user";
```

<!--
Exclude  
Crea un nuevo tipo excluyendo tipos específicos de otro tipo.
-->

---
transition: slide-up
layout: two-cols
level: 2
---

# Discriminated

- Discriminated Union
- Different possible attributes.

::right::

```ts
type RoleAttributes =
  | { role: "admin"; orgId: string }
  | { role: "user" }
  | { role: "anonymous" };
```

<!--
Discriminated  
Podemos discriminar y tener distintos atributos.
-->

---
transition: slide-up
layout: two-cols
level: 2
---

# Extract\<T, K\>

- Extract\<T, K\>
- Used to create a new type by including specific types from another type.

```ts
type Extract<T, U> = T extends U ? T : never;
```

::right::

```ts
type RoleAttributes =
  | { role: "admin"; orgId: string }
  | { role: "user" }
  | { role: "anonymous" };

type AdminRole = Extract<
  RoleAttributes,
  {
    role: "admin";
  }
>;
```

```ts
type AdminRole = {
  role: "admin";
  orgId: string;
};
```

<!--
Extract  
Se utiliza para crear un nuevo tipo incluyendo tipos específicos de otro tipo.
-->

---
transition: slide-up
layout: two-cols
level: 2
---

# NonNullable\<T\>

- NonNullable\<T\>
- Creates a new type by excluding null and undefined from a given type.

```ts
/**
 * Exclude null and undefined from T
 */
type NonNullable<T> = T & {};
```

::right::

```ts
type MaybeString = string | null | undefined;

type DefinitelyString = NonNullable<MaybeString>;
```

```ts
type DefinitelyString = string;
```

<!--
NonNullable  
Crea un nuevo tipo excluyendo null e undefined de un tipo dado.
-->

---

# Utility Types: Functions

- Function
- ReturnType
- Parameters
- Promise
- Awaited

<!--

-->

---
transition: slide-up
layout: two-cols
level: 2
---

# Functions

- Functions
- Parameters
- ReturnType

::right::

```ts
type Func = (a: number, b: string) => number;
```

<!--
Funciones  
Tienen parámetros
Tiene un tipo de retorno
-->

---
transition: slide-up
layout: two-cols
level: 2
---

# ReturnType\<T\>

- ReturnType\<T\>
- Extracts the return type of a function. 
- Useful when we want to work with higher-order functions.

```ts
type ReturnType<T extends (...args: any) => any> = 
  T extends (...args: any) => infer R ? R : any;
```

::right::

```ts
type Func = (a: number, b: string) => number;

type ReturnValue = ReturnType<Func>;
```

```ts
type ReturnValue = number;
```

<!--
ReturnType  
Extrae el tipo de retorno de una función.  
Útil cuando queremos trabajar con funciones de orden superior.
-->

---
transition: slide-up
layout: two-cols
level: 2
---

# Parameters\<T\>

- Parameters\<T\>
- Extracts the parameter types from a given function type.
- Simplifies code by making it easy to work with functions without manually specifying argument types.

```ts
type Parameters<T extends (...args: any) => any> = 
  T extends (...args: infer P) => any ? P : never;
```

::right::

```ts
type Func = (a: number, b: string) => number;

type Params = Parameters<Func>;
```

```ts
type Params = [a: number, b: string];
```

<!--
Parameters  
Extrae los tipos de parámetros de un tipo de función dado.  
Simplifica el código facilitando el trabajo con funciones sin especificar manualmente los tipos de argumentos.
-->

---
transition: slide-up
layout: two-cols
level: 2
---

# Promise\<T\>

- Promise\<T\>
- Represents a value that may be available asynchronously in the future.
- It's a fundamental type for working with asynchronous operations.

::right::

```ts
type PromiseString = Promise<string>;
```

<!--
Promise  
Representa un valor que puede estar disponible de forma asíncrona en el futuro.  
Es un tipo fundamental para trabajar con operaciones asíncronas.
-->

---
transition: slide-up
layout: two-cols
level: 2
---

# Awaited\<T\>

- Awaited\<T\>
- Extracts the resolved type from a promise.
- Simplifies working with promises and helps avoid manual type annotations.

::right::

```ts
type PromiseString = Promise<string>;
type Result = Awaited<PromiseString>;

type PromiseNumber = Promise<number>;
type Result2 = Awaited<PromiseString>;
```

```ts
type Result = string;

type Result2 = number;
```

<!--
Awaited  
Extrae el tipo resuelto de una promesa.  
Simplifica el trabajo con promesas y ayuda a evitar anotaciones manuales de tipo.
-->

---
layout: new-section
---

# Demo

![Demo](https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExYmI4ZWVlNTUyOTBiZmU0ZDlkNGIwZGRkNTc4NzI3M2VhNmZjOWQ4MSZlcD12MV9pbnRlcm5hbF9naWZzX2dpZklkJmN0PWc/d9O5lPyufbSfZzC1pq/giphy.gif)

---
layout: end
---

# QA

![QA](https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExYzA2NjNmZmQ2NjdhNTdiMWRiYzcyOGMxMWM5OTZlMzFiNWE3YzZkOCZlcD12MV9pbnRlcm5hbF9naWZzX2dpZklkJmN0PWc/xT5LMB2WiOdjpB7K4o/giphy.gif)