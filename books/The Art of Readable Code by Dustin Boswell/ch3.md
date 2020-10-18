# The Are of Readable Code by Dustin Boswell

## Chapter 3: Names That Can’t Be Misconstrued

### Key Summary
As in the previous chapter, `PACKING INFORMATION INTO NAMES`, we are asked to **review the names from the perspective of other's to avoid ambiguity**.

- Method: Use a proper name, so users can know the operation is expensive or not.
- Boolean: Add `is`, `has`, `can`, or `should` to be precise. Avoid negated terms.
- Range: Be precise for inclusive or exclusive terms.

### Note

The readability actually arises above names. For functions, it's the signature.

There are several way to interpretate a variable, a function, a parameter for a functions, and etc,.

1. Names
2. Parameters
3. What does it do?
4. What is it for?

#### We have several examples for function's name.

- `Filter()`
- `Clip(text, length)`

Filter can either be a whitelist or a blacklist. Clip as a verb may be to preserve a length of text or to cut out a length of text from the end.

**Reason**: the ambiguous of names.

`Select` or `Exclude` can be used instead of `Filter`. `Truncate` can be used instead of `Clip`.

#### The signature of `Clip(text, length)` is also ambiguous.

In several languages, a rune may take more than byte. The length and bytes may not be equaled. `max_word` may also be another interpretation.

**Be precise.**
**Be precise.**
**Be precise.**

##### Again, `limit` is ambiguous. `Max` and `Min` is not.

Prefer inclusive limit. Naming it to max and min is the clearest way.

#### Range... it is a first-last range or begin-end range?

Use precise naming for each situations.

- max
- min
- first
- begin

are inclusive.

- stop
- end

are exclusive. begin/end is ambiguous, but it's already an idiomatic in programming world.

#### Booleans, add `is`, `has`, `can`, or `should` to be precise

Avoid negated terms.

### Beyond Names, the expectation from user

`Get` is inexpensive to users. Use `Compute` instead if it's not a trivial operation.

`Size` or `length` are usually expected to be a constant. Use `Count` instead.

**Use a proper name, so users can know the operation is expensive or not.**
