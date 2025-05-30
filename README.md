<!---
{
  "author": "Stephan Bökelmann",
  "first_used": "2025-04-02",
  "keywords": ["Functions", "Cardinality", "Datatypes", "Mengenlehre", "C Language"]
}
--->

# Cardinality, Functions and Datatypes

## 1) Introduction
> 🧮 Understanding the size of sets helps us reason about the behavior of functions in programming.

In mathematics, the **cardinality** (or **mächtigkeit**) of a set describes how many elements it contains:
- `|{1,2,3}| = 3`
- `|ℕ| = ℵ₀` (countably infinite)
- `|ℝ| > ℵ₀` (uncountably infinite)

In C, every **datatype** defines a set of possible values — and those sets are always **finite**.

For example:
- `char` uses 8 bits → `|char| = 2^8 = 256`
- `int` uses 32 bits → `|int| = 2^32 = 4,294,967,296`
- `bool` is conceptually just `|bool| = 2`

This gives us a tool to reason about **functions**:
```c
int add(int a, int b);
```
is a function from:
```
int × int → int
```
with:
- input space: `2^32 × 2^32 = 2^64`
- output space: `2^32`

This means: the function cannot be injective — different inputs may yield the same output.

Remember: Every C [function](https://github.com/STEMgraph/0b6b3ce8-418e-4900-ae42-a6d068389a12) defines a mapping from the [Cartesian product](https://github.com/STEMgraph/e954e47f-3d9d-4707-bea3-1ef3105278f4) of its parameter types to its return type.

## 2) Tasks
1. **Count Values**: For the following types, compute the number of possible values:
   - `uint8_t`
   - `int16_t`
   - `bool`
   - `float` (estimate based on IEEE 754, not exact)

2. **Function Domains**: Write a function `bool is_zero(uint8_t x);` and describe the cardinality of its input- and output-sets.

3. **Write a Surjective Function**: Write a function `bool parity(uint8_t x);` that maps even numbers to `0`, odd to `1`. Is this function surjective?

4. **Write a Constant Function**: Write a function `int always_five(float x);` that ignores the input. Argue about its injectivity and surjectivity.

5. **Collision Observation**: Write a function `uint8_t compress(uint32_t x);`. Try calling it with two different values.

## 3) Questions
1. What does it mean for a function to be injective, surjective, bijective?
   Injective means different inputs produces different outputs, surjective means every element from Domain is mapped to element in codomain, bijective means combination of both.
3. Can a function in C be truly bijective if the domain is larger than the codomain?
   Nope, function to call injective must be maped to uniq element in B.
5. Why do collisions matter in hashing?
   if 2 strings get the same value as hashvalue it means 1 of the string isnt mapped anymore.
7. What’s the difference between a function that *ignores* its argument and one that *uses* it partially?
   if we ignoring argument of a function the output might be the same, if we use argument partially we can have different input but with the same output.
9. How does knowing the cardinality of types help in optimizing or verifying code?
    If the Compiler knows in uint8_t we can have maxvalue 2^8, and we use in our code for value 3 Datatype int, compiler can optimize our code and execute it faster.

## 4) Advice
Use `sizeof(type)` and `<stdint.h>` types to make reasoning about value ranges easier. When debugging unexpected results, ask yourself: *how many inputs exist, and how many outputs are possible?* This can lead directly to understanding bugs in conversions, hashing, or logic.

