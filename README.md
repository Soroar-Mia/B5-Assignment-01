##**What are some differences between interfaces and types in TypeScript?**##

These two tools which provide the strongest aid to helping describe data structures are the interface and type. They might seem the same initially, and in many cases they are. But, with all things TypeScript, there are noticeable differences that can affect the code architecture and maintenance.

Interface

As the name suggests, an interface defines the shape of an object. As you may have guessed, it is used to describe contracts for purposes of class based Object Oriented Programming and it is centered around objects and classes that are to be created or implemented.

interface User {
  name: string;
  age: number;
}


Type Alias

A type alias can be used to give a new name to any type, and not just objects, creating new possibilities for defining types. Primitive types, unions, tuples, functions, and many other things can be aliased.

type User = {
  name: string;
  age: number;
};

Extension and Composition

Interfaces support extension via the extends keyword.

interface Animal {
  name: string;
}
interface Dog extends Animal {
  breed: string;
}

Types support composition via intersection (& operator).

type Animal = { name: string };
type Dog = Animal & { breed: string };

Declaration Merging

One powerful feature of interfaces is declaration merging—you can define the same interface multiple times, and TypeScript merges them.

interface Person {
  name: string;
}
interface Person {
  age: number;
}

Type aliases do not support this:
type Person = { name: string };
Error: Duplicate identifier if you declare 'type Person' again


Use with Unions, Intersections, Tuples, and Primitives.

Type aliases shine when you need more flexibility. You can describe:

Union types,Primitive aliases,Tuples,Function signatures

type Status = "loading" | "success" | "error";
type Point = [number, number];
type Add = (a: number, b: number) => number;
Interfaces cannot do this. Use type when modeling non-object data or combining multiple structures.

Readability and Tooling

Interfaces offer better readability and integration with tools like autocompletion and API documentation generators. They tend to be favored in public library APIs.

interface User {
  id: number;
  email: string;
}

Type aliases are more suited for advanced type operations, especially in modern TypeScript.


**##What is the use of the keyof keyword in TypeScript? Provide an example.##**


TypeScript gives developers the power to write safer, more expressive code by adding strong typing on top of JavaScript. Two incredibly useful features in its type system are union types and intersection types. These advanced types let you build flexible and precise type definitions, making your code more robust and readable.

In this blog post, we’ll explore what union and intersection types are, why they matter, and how to use them effectively—with clear, real-world examples.

What Are Union Types?
A union type allows a variable to hold more than one possible type. It’s like saying: “this value can be one or another.”

type A = string | number;
This means a variable of type A can be either a string or a number.

Real-World Example:
Imagine a function that takes either a string or a number as input and returns its string form:

function formatInput(input: string | number): string {
  return input.toString();
}

console.log(formatInput("Hello")); 
console.log(formatInput(123)); 
Here, input is a union of string | number, allowing flexibility while still providing type safety.
 What Are Intersection Types?
An intersection type combines multiple types into one. It’s like saying: “this value must satisfy both types.”

type A = { name: string };
type B = { age: number };

type C = A & B;
Now, type C must have both name and age.

Real-World Example:
Let’s say we’re working with user profiles that must contain personal info and account data:

type PersonalInfo = {
  name: string;
  email: string;
};

type AccountInfo = {
  username: string;
  password: string;
};

type User = PersonalInfo & AccountInfo;

const newUser: User = {
  name: "Alice",
  email: "alice@example.com",
  username: "alice123",
  password: "securepassword"
};
This ensures that a User must contain all the fields from both PersonalInfo and AccountInfo.

Combining Union and Intersection
You can even nest union and intersection types for complex type structures.

type Admin = { role: "admin"; accessLevel: number };
type Editor = { role: "editor"; tools: string[] };
type User = { id: number; name: string };

type AdminUser = User & Admin;
type EditorUser = User & Editor;

type SystemUser = AdminUser | EditorUser;

const user1: SystemUser = {
  id: 1,
  name: "John",
  role: "admin",
  accessLevel: 5
};

const user2: SystemUser = {
  id: 2,
  name: "Jane",
  role: "editor",
  tools: ["Photoshop", "Illustrator"]
};
Here, SystemUser is a union of two intersections, allowing for multiple user types in a single system—each with shared and unique properties.

Union and intersection types are vital tools for crafting flexible, scalable, and type-safe applications in TypeScript. Whether you’re building a small app or a large-scale system, understanding and leveraging these types gives you a powerful edge in modeling real-world data structures.

By thinking in terms of "or" with unions and "and" with intersections, you can write cleaner, smarter, and more maintainable TypeScript code.
