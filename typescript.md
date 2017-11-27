# TypeScript

## References

* [Learn TypeScript in Y Minutes](https://learnxinyminutes.com/docs/typescript/)
* [TypeScript Deep Dive](https://www.gitbook.com/book/basarat/typescript/details)

## Tools
- [A minimal Yeoman Generator for creating NodeJS modules using TypeScript](https://github.com/ospatil/generator-node-typescript#readme)

## TpyeScript Notes/Tips/Patterns

* Scope: by default members in a class are **public**
* **Enum**: an enum is a way of giving more friendly names to sets of **numeric** values
  * String enum: use custom Type. See [more here](https://basarat.gitbooks.io/typescript/content/docs/types/literal-types.html).
* Do we put return type when defining function?  
  Yes. `getSum(a: number, b: number): number {}`

* Type assertion: `(<string>someValue).length;`

* We have `static`, `readonly`
  * `const` is for varibale. No one can modifiy it after assigned.
  * `readonly` is for property (class property to property in interface). Properties must be initialized **at their declaration or in the constructor**. It only ensures that it won't be modified by me. Others can still modify it. [See here](https://basarat.gitbooks.io/typescript/content/docs/types/readonly.html)
  * `static` must be class member.

* Function overload, this is possible in TypeScript but it's not supported by JavaScript.
* Default paramter: `getSum(data: number[], skipNegative: boolean = false)`

#### Favor getter over method in TS

#### How to declare type to object property and key?
```ts
var stuff: { [key: string]: string; } = {};
stuff['a'] = ''; // ok
stuff['a'] = 4;  // error
```
#### Use Destructuring (FP concept)
```ts
// pick only the data we need using destructing
// Function signature: getAccountInfo(): {balance: number; cardStatus: string; cardNumber: string; cardHolder: string}

// before:
.then((response:any) => {
        const data = this.getAccountInfo()
        return {
          balance: data.balance,
          cardStatus: data.cardStatus
        };

// after
.then((response:any) => {
        const {balance, cardStatus} = this.getAccountInfo()
        return {
          balance,
          cardStatus
        };
```

#### Be careful: it's too easy to create private member
If the data is NOT used anywhere, don't put private.

```ts
constructor(private data?: any) {
      this.model = this.extract(data);
    }
```




