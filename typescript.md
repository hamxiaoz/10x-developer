# TypeScript

### References

* [Learn TypeScript in Y Minutes](https://learnxinyminutes.com/docs/typescript/)
* [TypeScript Deep Dive](https://www.gitbook.com/book/basarat/typescript/details)

### Tools
- [A minimal Yeoman Generator for creating NodeJS modules using TypeScript](https://github.com/ospatil/generator-node-typescript#readme)

### Notes

* Scope: by default members in a class are **public**
* **Enum**: an enum is a way of giving more friendly names to sets of **numeric** values
  * String enum: use custom Type. See [more here](https://basarat.gitbooks.io/typescript/content/docs/types/literal-types.html).
* Do we put return type when defining function?  
  Yes. `getSum(a: number, b: number): number {}`

* Type assertion: `(<string>someValue).length;`

* We have `static`, `readonly`

  * If you want to express **constant**, use `readonly` or `static readonly`.
  * `readonly` properties must be initialized **at their declaration or in the constructor**.

* Function overload, this is possible in TypeScript but it's not supported by JavaScript.
* Default paramter: `getSum(data: number[], skipNegative: boolean = false)`

* Destructing

  ```typescript
  // pick only the data we need using destructing
  // Function signature: getAccountInfo(): {balance: number; cardStatus: string; cardNumber: string; cardHolder: string}
  const {balance, cardStatus} = this.getAccountInfo();
  ```



