# Guard assertions in Javascript

One of the refactoring in the book Refactoring second edition by Martin Fowler is "[Introduce Assertions](https://refactoring.com/catalog/introduceAssertion.html)".

I have not seen many example of this beign used in the Javascript code bases. 

Suppose a function that look a score of some sort existed and returned a rating out of 5.

```javascript
const rating(score) {
	return Math.ceil(score / 20);
}
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMzMDgyODM0XX0=
-->