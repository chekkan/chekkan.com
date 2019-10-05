# Guard assertions in Javascript

One of the refactoring in the book Refactoring second edition by Martin Fowler is "[Introduce Assertions](https://refactoring.com/catalog/introduceAssertion.html)".

I have not seen many example of this beign used in the Javascript code bases. 

Suppose a function that look a score of some sort existed and returned a rating out of 5.

```javascript
function rating(score) {
	return Math.ceil(score / 20);
}
```

Although at first glance, this function looks simple, it has made a lot of assumption about its input argument. The obvious assumption is that the score is between 1 and 100.  The not so obvious assumpution is that is indeed a number. As javascript is a non typed language, any client calling this rating function is allowed to pass in score as `"21"` or even `"foo"`.

What should the return value of this function be if the input `score` is a string? 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI2Mzk1MzQ2OV19
-->