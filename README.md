# TypeScript-Cheatsheets


### Interface

> Interface Define the shape and structure of objects or variables.

```javascript
interface InterfaceUserBase {
  username: string;
  age: number;
}
```

### Interface Extends

> Interfaces can be extended using the extends keyword to inherit properties and methods from other interfaces.
> Extends is used for type constraint and inheritance in TypeScript.

```javascript
interface InterfaceUserProfile extends InterfaceUserBase {
  followers: number;
}
```

### Type

> Type Define the shape and structure of objects or variables.

```javascript
type TypeUserBase = {
  username: string;
  age: number;
};
```

### Type aliases

> Type aliases (types) cannot be extended with the extends keyword but can be composed and combined using intersection (&) and union (|) operators to create more complex types.

```javascript
type TypeUserProfile = TypeUserBase & { followers: number };
```

### Never

> never type represents values that will never occur or be reached during the execution of a program.

```javascript
const neverValue: never = (() => {
  throw new Error("This should never happen!");
})();
```

### Void

> void is a type indicating the absence of a return value.

```javascript
const voidMethod = () => {
  console.log("Hello, world!");
}

const result = void voidMethod();
// Output: undefined
```

### Array

> Array of objects can be represented as array of premitives, objects and .etc or generic type.

```javascript
type TypeArray: string[] = ['string', 'string'];

type TypeUserBase = {
  username: string;
  age: number;
}[];
```

OR

```javascript
type TypeArray: Array<string> = ['string', 'string'];

type User = {
    username: string,
    age: number
}
const UserBase: Array<User> = [
  {
    username: "string",
    age: 1
  }
];
```

### Index Signatures

> Index Signatures allow to write key with demand type.

```javascript
type TypeArray = {
  [key: number]: string;
}
```

### Union

> Intersection type combine together types and create single type.

```javascript
type TypeUnion = UserBase | UserProfile;
```

### Intersection

> Union type describes a value that can be one of several types.

```javascript
type TypeIntersection = UserBase & UserProfile;
```

### Const assertions

>  Properties of objects and elements of arrays can be made read-only.

```javascript
const UserBase = {
  username: string,
  age: number
} as const;
```

### Typeof operator

> typeof is used to retrieve the type of a value or variable.

```javascript
const data = [];
type DataType = typeof data;
// DataType is 'array'
```

### Conditional Types

> Conditional types allow you to create types based on conditions.
> Extends is used for type constraint and inheritance in TypeScript.
> Evaluates to boolean if the type T is an string.
 
```javascript
type Data<T> = T extends string ? boolean : number;

type ResultA = Data<string>;
// ResultA is boolean

type ResultB = Data<number>;
// ResultB is number
```

> Evaluates to never if the type T[] is an empty array.

```javascript
type Array<T> = T[] extends [] ? never : T[];

type ArrayCheck = Array<string>;
// ArrayCheck is string[]

type NonArrayCheck = Array<string | number>;
// NonArrayCheck is never
```

### Indexed access

> Indexed access in TypeScript, represented as T[K], retrieves the type of property K in object type T.

```javascript
type User = {
  name: string;
};

const user: User = {
  name: "David"
};

type NameType = User["name"];
// NameType is string

const name: NameType = "Kern";
```

## Mapped types

> Mapped types in TypeScript transform or create new types based on existing types.

### Keyof operator

> keyof is used to get the union of keys from an object type.

```javascript
type UserBase = {
  name: string;
  age: number;
};

type UserBaseKeys = keyof UserBase;
// UserBaseKeys is "name" | "age" 
```

### In operator 

> k in obj in TypeScript iterates over object keys for operations or creating new types.

```javascript
type Index = "a" | "b" | "c";
type FromIndex = {
  [K in Index]: number
};
```

### In keyof operator

> in keyof is a construct used to iterate over the keys of an object type.
> It allows you to add or define new types based on those keys.

```javascript
type User = {
  name: string;
  age: number;
};

type UserInfo = {
  [K in keyof Person]: string;
};

const person: PersonInfo = {
  name: "David",
  age: "30", // Error: Type 'string' is not assignable to type 'number'.
};
```
 
## Generic Types

> Generic types in TypeScript allow creating reusable types parameterized by different types.

### Examples

> Generic type of value

```javascript
interface GenericType<T> {
  data: T;
};
```

> Generic type of property

```javascript
interface GenericDataInterface<T> {
  (data: T): void;
}
```

> Generic type of array value

```javascript
interface GenericListInterface<T> {
  listData: T[];
}
```

> Generic method 

```javascript
const genericMethod = <T>(data: T): T => {
  return data;
};
```

> Extends keyof is used to constrain a generic type to specific object keys.

```javascript
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const User = {
  name: "David",
  age: 30,
};

const nameValue = getProperty(User, "name");
console.log(nameValue); // Output: "David"

const ageValue = getProperty(User, "age");
console.log(ageValue); // Output: 30
```

## Utils

### ReturnType

> ReturnType in TypeScript retrieves the return type of a function.

```javascript
type Method = () => boolean;
type MethodReturnType = ReturnType<Method>;
// MethodReturnType is boolean
```

OR

```javascript
type AsyncFunc = () => Promise<number>;
type FetchDataReturnType = ReturnType<AsyncFunc>;
// FetchDataReturnType is Promise<number>
```

### Pick

> Pick is a utility type that selects specific properties from a given type.

```javascript
type User = {
  name: string;
  age: number;
  data: [];
};

type UserInfo = Pick<User, 'name' | 'age'>;
// UserInfo is { name: string; age: number; }
```

### Omit

> Omit utility type in TypeScript creates a new type by excluding specified properties from an existing type.

```javascript
type User = {
  name: string;
  age: number;
  data: [];
};

type UserInfo = Omit<User, 'data'>;
// UserInfo is { name: string; age: number; }
```
