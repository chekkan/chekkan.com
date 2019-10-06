# Guard assertions in Javascript

Suppose a function that took a score of some sort existed and returned a rating out of 5.

```javascript
function rating(score) {
	return Math.ceil(score / 20);
}
```

Although at first glance, this function looks simple, it has made a lot of assumption about its input argument. The obvious assumption is that the score is between 1 and 100.  The not so obvious assumpution is that it is indeed a number. As javascript is an un-typed language, any client calling this rating function is allowed to pass in score as `"21"` or even `"foo"`.

What should the return value of this function be if the input `score` is a string? Should it return `NaN`? throw an exception? or return `-1`? 

It may be that in the context where this function is beign used, it will never get into the erronous state I've listed above. For example, `rating(toPercentage(score, 1, 10))`. Lets assume that `toPercentage` is returning a percentage given a score between `1` and `10`. So, in this context we can see that the function `rating` is actually beign used to covert a score from 1 to 10 to 1 to 5. Perhaps, `toPercentage` handles the case when the initial score variable is not a number between 1, to 10 (by capping the value), or the case when score is a string returning 0 etc. We don't know without looking in the source code of the function. the `toPercentage` function could even be provided by an `npm` package maintained by a different team, whom you don't trust to do the right thing. Who knows, they might start returning you percentage as a string in later versions. 

How would you know if the `score` variable 

How about writting these assumptions down?

```javascript
function rating(score) {
	console.assert(not(isNil(score)), "expected score to be not null or undefined");
	console.assert(Number.isFinite(score), "expected score to be a valid number");
	console.assert(score >= 1 && score <= 100, "expected score to be between 1 and 100");
	return Math.ceil(score / 20);
}
```

This is starting to look a lot like [defensive programming](https://en.wikipedia.org/wiki/Defensive_programming). It states that "a method should always validate its input". This is documented in the Reactoring book by Martin Fowler and he calls this refactoring "[Introduce Assertions](https://refactoring.com/catalog/introduceAssertion.html)". This seems a bit verbose and the lines of code has gone from 1 to 4.

```javascript
function rating(score) {
	assert.isBetween(1, 100, "score", score);
	return Math.ceil(score / 20);
}
```

In this variantion, `assert.isBetween` function can handle the assertion of the score beign `undefined` or `null`, also ensuring the type beign a number and finally the acceptable range. 

```javascript
function isBetween(lower, upper, name, value) {
	console.assert(not(isNil(value)), `expected ${name} to be not null or undefined`);
	console.assert(Number.isFinite(value), `expected ${name} to be a valid number, but was ${value}.`);
	console.assert(value >= lower && value <= upper, `expected ${name} to be between ${lower} and ${upper}.`);
}
```

If a more granular control is requires, we could compose these functions together...

```javascript
function rating(score) {
	const ensure = 
	assert.notNil("score", score) && 
	assert.isFinite("score", score) &&
	assert.isBetween(1, 100, "score", score);
	return Math.ceil(score / 20);
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIyMzY5NDA4LDEwNDU5OTQyNjIsLTE1MD
I0MDk5MzYsODQ3NzI1OSwtMjYzOTUzNDY5XX0=
-->