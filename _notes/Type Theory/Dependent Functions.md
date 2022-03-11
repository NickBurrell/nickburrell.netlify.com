---
title: Dependent Functions
tags: Type-Theory Dependent-Functions
season : summer 
---

A **depenedent function** is a function who's return type can depend on the inputs it recieves. For instance, in Idris, it is possible to write the following.
```haskell
dupElem : Vect n a -> Vect (2*n) a
dupElem : [] -> []
dupElem : (x::xs) = x :: x :: dupElem xs
```
Notice that here, the type `Vect` has a parameter `n`, which is *not* a type, in fact, it is a value of type `Nat`. This has many useful applications, especially to ensuring type safety. For instance, in many applications in C++, we use `std::vector` to store dynamic length arrays. Thankfully, there are many facilities in C++ to prevent reading garbage heap data, but its very easy, especially for new developers, to forget. Using something like `std::array` is inconvinient, because you need to break the value/type barrier for parameters, and end up with mixed functions like
```cpp
template<typename T, std::size_t n> auto doThing(std::array<T, n> p) {
	// . . .
}
```
While this is completely fine, and very correct in many cases, it *feels* less natural, like blending two different aspects of the language. To recreate the Idris example in C++, we would need a function along the lines of
```cpp
template<typename T, std::size_t n> auto doThing(std::array<T, n> p) {
	std::array<T, 2*n> arr();
	for(std::size_t i = 0u; i < n; ++i) {
		arr[2*i] = p[i];
		arr[2*i+1] = p[i];
	}
}
```
While both versions are very natural, there is an elegance to the first definition. There is no mixing of metaprogramming and normal functions, just a single unified definition.