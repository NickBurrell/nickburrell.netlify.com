---
title: Dependent Types in C++
tags: C++ Type-Theory Dependent-Functions
season : summer
content-type: article
---

Many people are aware of how incredible the C++ type system is. There are numerous examples of very idiomatic and clean code using templates, and in modern C++, concepts, to achieve what can only be dreamed of in other languages. Some great examples include `std::array`, `std::iterator`, and more. Few people though are aware of some newer features added in C++20. Since C++11, developers have been allowed to use *non-type* template arguments. An example of this is the definition of `std::array`, which looks similar to the definition below.
```cpp
template<typename T, std::size_t N> array {
	// . . .
}
```
Here, the parameter `N` is the number of elements in the array. Prior to C++20, these were restricted to what are called *literal types*, which can be thought of as relatively simple, plain old data types. A more precise definition can be found [here](https://en.cppreference.com/w/cpp/named_req/LiteralType). For the purpose of this article, we will just assume a few basic principles these types may satisfy, namely:
- Default or trivial destructor
- Reference types
- Scalar types
- Closures (anonymous functions)
- Classes/Structs, where all members are literal types

With that in mind, it would be constructive to move on to an example.
## A More Complicated Example
Lets begin by defining a rather strange type, `Foo`.
```cpp
template<auto> struct Foo;

template<auto X> requires (X < 4) struct Foo<X> {
	using result_type = int;
};

template<auto X> requires (X >= 4) struct Foo<X> {
	using result_type = std::bool;
};
```
This type looks rather odd, right? I mean, it is clearly a template specialization, using a concept to specialize, but what is the point of this type? Well, it allows us to write functions like this.
```cpp
template<auto X> constexpr auto DoThing(FooR<X> p) {
	if constexpr (X < 4) {
		return p*p;
	} else {
		return !p;
	}
}

// Both of these assertions pass!
static_assert(DoThing<3>(4) == 16);
static_assert(DoThing<5>(false) == true);

```
A very natural question to ask now would be why? Well, this is just the groundwork a wide array of possible programs that can be written in C++, with the understanding that if you saw this during a code review at your business, you would need to have a long talk with the developer.
This is an example of a [[_notes/Type Theory/Dependent Functions \|dependently typed function]], which has a rich history in functional programming and theorem proving languages, though is rarely seen outside that sphere of influence. It is very interesting then that C++ would incorporate such a feature, but given C++'s history of developments with metaprogramming, it was inevitable, though I am unsure if this was their intent long term. Regardless, it is nice to have even the potential to use such a powerful tool in such a mainstream language.
## Limitations and Further Work
As can be seen above, there is some unfortunate nuance to how these dependent functions can be used. Namely, all parameters used must be template parameters. For instance, there is no way to write a function like
```cpp
constexpr auto f(auto x) -> Foo<x> {
// . . .
}
```
When a value is taken as a function parameter, it must stay as a function parameter. This introduces an interesting "tiering" to the type system; you can always take a type-level parameter and move it into a value-level parameter, but never the other way around. 
In spite of this, it is still useful to consider *compile-time* C++ to be dependently typed, as you can still do a number of amazing things, which I plan to expand on in later posts (including potential theorem-proving properties!) With all this said, I will leave off with a little teaser of whats to come...
```cpp
template<auto X> struct Lit { };
template<typename ... > struct EqT;

template<auto X, auto Y> requires std::is_same_v<Lit<X>, Lit<Y>> 
	struct EqT<Lit<X>, Lit<Y>> { };
```