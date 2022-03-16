---
title: Equality Types in C++
tags: C++ Type-Theory
type: article
status: ongoing
toc: true
trello_board_card_id: 62308264081f3d842fd0d78e;623082e24327ff0cfbea2f36
trello_plugin_note_id: FqtjxBDFhpZXwwRly8q2K
---
# Introduction
In type theory, and in general theorem proving, the notion of equality is a rather nuanced matter. For instance, there is at least two generally accepted forms of equality: definitional equality and value equality. Most of us are very familiar with the second, and could probably figure out what the first means. Programming languages tend to operate the same way; there is a strong notion of value equality, and almost no context for definitional equality.

# Type-Level and Value-Level Functions
Before we can really begin any development of equality and equality types, we need to expand on a notion we began with in the [[_articles/Dependent Types in C++\|previous article]]. Its also important to consider that we are in this case only talking about C++, as these concepts don't quite transfer over one-to-one into real dependently typed languages like Idris. 
## Value-Level Functions
To make things simple, we start with *value-level* functions. These are your every day, run-of-the-mill functions, like `x+2`, or `Console.WriteLine(...)`. They are functions that take in values, and return values, with types that are defined *long* before evaluation. As a concrete example, consider the following.
```cpp
	int square(int p) {
		return p*p;
	}
```
This isn't a particularly flashy function, nor does it need to be to illustrate the point: value-level functions are very simple objects conceptually.

## Type-Level Functions
This is where things get slightly more complicated, and if you aren't comfortable with modern C++ metaprogramming concepts like templates, it would be best to brush up on those and come back later. 

We begin by defining a *type-level* function. Put simply, a type-level function is a *type* that takes in both types and values, and produces either a type or a value. To those with a background in type theory, or who are familiar with Idris, Agda, or Coq, you may think that this sounds a lot like the definition of a [[_notes/Type Theory/Dependent Functions\|dependent function]], and you'd be right! Unfortunately, due to limitations in C++ noted in the last article, we have to make a deliniation between dependent functions and regular functions.

To give a concrete example of what we mean, let's translate the function above into a type-level function.
```cpp
	template<int p> struct SquareT { const int val = p*p; };
```
This may look a bit cumbersome, and perhaps even pointless, but rest assured, this will become useful to us later. 
It is also worth noting that you *can* use value-level functions inside of type-level functions. The only requirement is that any parameters to value-level functions must be type-level parameters, such as the example above. Additionally, as stated above, type-level functions can return both  values *and* types (for an example, see [[_articles/Dependent Types in C++#A More Complicated Example\|here]]), which can make them a bit difficult to deal with in terms of function signatures. Unfortunately, I know of no simple way to deal with this, so caution must be exercised by the developer.

# Equality Types
We are now ready to move onto defining equality and equality types, but first, we introduce a few more pieces of machinery to make our lives easier. Namely, we introduce the `Reduce` type, which will become very important later, when developing proof trees. Reduce is simply defined as follows.
```cpp
template<typename ...> ReduceInner;

template<typename ... Ts> using Reduce = ReduceInner<...Ts>::result;
```
Note that this is just a forward declaration and a using clause, which while on the surface seems rather superfluous, we expand on shortly, and then the real magic happens. 

## The `Val` Type
Now that all of the pieces are in place, we finally define our equality type.
```cpp
template<auto X> Val { };
```
I know, I know. "That's it? Thats what we've been building up to?" you may ask yourself. The answer is yes. There *is* one important thing to see here: this type has *exactly* one inhabitant: itself. By inhabitants, we really mean how many unique ways there are to instantiate a type. A simple example is `bool`, as there are exactly two inhabitants: `true` and `false`. This notion is very important in type theory, especially with regards to the Curry-Howard Correspondance, but that is a can of worms for another time.

What is really important here is the semantics of `Val`. It operates on *definitional* equality, not *value* equality. To illustrate what we mean, consider the following example.
```cpp
struct Foo {
	int v;
	constexpr Foo(int d): v(d) {}
	constexpr auto operator==(const Foo& other) const -> bool { return true; }
};

template <Foo d1, Foo d2>
	requires std::is_same_v<Val<d1>, Val<d2>>
constexpr auto test(const Valeral<d1>& l1, const Valeral<d2>& l2) -> void {
	std::cout << "The two are equal!" << std::endl;
}
int main(void) {
	Valeral<Foo(0)> v1;
	Valeral<Foo(1)> v2;
	test(v1, v2);
}
```
Based on the definition above, clearly `Foo(0)==Foo(1)`, but this code does not compile! This is because `Val<Foo(0)>` and `Val<Foo(1)>` do NOT represent the same type. Though, using a negative example is only so helpful, as this only serves to show negative cases. A positive case may be more constructive.
```cpp
static_assert(std::is_same_v<Val<2>, Val<1+1>>);
```
This assertion will not be thrown, as `Val<2>` and `Val<1+1>` are in fact the same type! 

While this sounds great, I must admit my testing of this is not as thorough as I would have liked. For instance, this has only been tested on simple structs and primitive types, and there has not been as much testing to properly determine what value-level functions are appropriate and resolve correctly inside the type-level parameter block in `Val`. This is something that does require further testing, and I am looking forward to exploring it more deeply.

## Equality Types
Now for the final act: equality. There is a reason we took so long building up to this, as we will see, but lets just dive into the definition.
```cpp
template<typename, typename> struct EqT;
template<auto X, auto Y> requires std::is_same_v<Val<X>, Val<Y>> 
	struct EqT<Val<X>, Val<Y>> { };
```

Lets take a moment to unpack what this is really saying. We start by forward declaring a templated type, `EqT`, with no way to instantiate it. Then, we define a *specialization* of it, where the specialization is only valid if, given the two input parameters, `X` and `Y`, the types `Val<X>` and `Val<Y>` are the same. That sentence was a touch long, so perhaps it's time for an example.
```
EqT<3, 4> eq_prf_1;
EqT<1, 2-1> eq_prf_2;
```
The above code won't compile, and by this point, it should be pretty clear why: $3$ and $4$ are not equal, while $1$ and $2-1$ are equal. As with the previous section, it may be difficult to see why this is useful. For most traditional software development, none of what has been discussed here is very applicable; this is not a design pattern, or an idiom that you should follow, merely a very interesting curiousity. However, to someone interested in type theory, this is fascinating, which we will cover at a later date.

# Conclusion
While a very interesting curiousity to explore, equality types in C++ will likely never catch on in mainstream use. They offer very little utility to people beyond those bold enough to explore theorem proving in the C++ type system. With that in mind, I still want to investigate this further. Though my research on this, I've written several basic proofs akin to those in introductory texts on languages like Idris and Coq. With that in mind, I leave off with another teaser of whats to come...
```cpp
template<typename T, std::size_t N, std::size_t M> requires Eq<N, M, 1>
constexpr auto array_proof(const std::array<T, N> k) noexcept -> std::array<T, M> {
	// . . .
}
template<typename T, std::size_t N, std::size_t M> requires Eq<N, M> && Neq<N, 1>
constexpr auto array_proof(const std::array<T, N> k) noexcept -> std::array<T, M> {
	// . . .
}
```