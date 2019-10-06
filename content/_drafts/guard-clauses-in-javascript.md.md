# Guard assertions in Javascript

One of the refactoring in the book Refactoring second edition by Martin Fowler is "[Introduce Assertions](https://refactoring.com/catalog/introduceAssertion.html)".

I have not seen many example of this beign used in the Javascript code bases. 

Suppose a function that look a score of some sort existed and returned a rating out of 5.

```javascript
function rating(score) {
	return Math.ceil(score / 20);
}
```

Although at first glance, this function looks simple, it has made a lot of assumption about its input argument. The obvious assumption is that the score is between 1 and 100.  The not so obvious assumpution is that it is indeed a number. As javascript is an un-typed language, any client calling this rating function is allowed to pass in score as `"21"` or even `"foo"`.

What should the return value of this function be if the input `score` is a string? Should it return `NaN`? throw an exception? or return `-1`? How about writting these assumptions down?

```javascript
function rating(score) {
	console.assert(not(isNil(score)), "expected score to be not null or undefined");
	console.assert(Number.isFinite(score), "expected score to be a valid number");
	console.assert(score >= 1 && score <= 100, "expected score to be between 1 and 100");
	return Math.ceil(score / 20);
}
```

This is documented in the Reactoring book by Martin Fowler and he calls this refactoring "Introduce Assertion". This seems a bit verbose and the lines of code has gone from 1 to 4.

```javascript
function rating(score) {
	assert.isBetween(1, 100, "score");
	return Math.ceil(score / 20);
}
```

In this variantion, `assert.isBetween` function can handle the assertion of the score beign `undefined` or `null`, also ensuring the type beign a number and finally the acceptable range. 

```javascript
function isBetween(lower, upper, name) {
	console.assert(not(isNil), `expected ${name} to be not null or undefined`);
	console.assert(Number.isFinite(score), `expected ${name} to be a valid number`);
	console.assert(
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExMTUyNzc4MTYsODQ3NzI1OSwtMjYzOT
UzNDY5XX0=
-->