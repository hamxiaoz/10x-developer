# TypeScript

References:

* [Learn TypeScript in Y Minutes](https://learnxinyminutes.com/docs/typescript/)
* [TypeScript Deep Dive](https://www.gitbook.com/book/basarat/typescript/details)

### Notes

* Class: by default members in a class are **public**
* **Enum**: an enum is a way of giving more friendly names to sets of **numeric** values
  * String enum: use custom Type. See [more here](https://basarat.gitbooks.io/typescript/content/docs/types/literal-types.html).
* Do we put return type when defining function? Yes. For example: `getSum(a: number, b: number): number {}`
* Type assertion: `(<string>someValue).length;`
* Yes, we have `static`, `readonly`
  * If you want to express **constant**, use `readonly` or `static readonly`.
* Function overload, this is possible in TypeScript but it's not supported by JavaScript.
* Do we have default parameters? Yes



