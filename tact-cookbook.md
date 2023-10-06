# Tact Cookbook

The core reason for creating the Tact Cookbook is to collect all the experience from Tact developers in one place so that future developers will use it!

Compared to the FunC Documentation, this article is more focused on everyday tasks every FunC developer resolve during the development of smart contracts.

## Basics
### How to write a Hello World smart contract

```
contract HelloWorld {

    get fun greeting(): String {
        return "hello world";
    }        

}
```

### How to generate a random number  


```tact
// Declare a variable to store the random number
let number: Int;

// Generate a new random number, which is an unsigned 256-bit integer
number = randomInt();

// Generate a random number between 1 and 12 
number = random(1, 12);
```

💡 Useful links
- [`randomInt()` in docs](https://docs.tact-lang.org/language/ref/random#randomInt)
- [`random()` in docs](https://docs.tact-lang.org/language/ref/random#random)


## Slice
### How to determine if slice is empty

`Slice` is considered *empty* if it has no stored `data` **and** no stored `references`.

Use `empty()` method to check if a `slice` is empty.

```tact
// Create an empty slice with no data and no refs
let empty_slice: Slice = emptyCell().asSlice();
// Returns `true`, because `empty_slice` doesn't have any data or refs
empty_slice.empty();

// Create a slice with some data
let slice_with_data: Slice = beginCell().
    storeUint(42, 8).
    asSlice();
// Returns `false`, because the slice has some data
slice_with_data.empty();

// Create a slice with a reference to an empty cell
let slice_with_refs: Slice  = beginCell().
    storeRef(emptyCell()).
    asSlice();
// Returns `false`, because the slice has a reference
slice_with_refs.empty();

// Create a slice with data and a reference
let slice_with_data_and_refs: Slice  = beginCell().
    storeUint(42, 8).
    storeRef(emptyCell()).
    asSlice();
// Returns `false`, because the slice has both data and reference
slice_with_data_and_refs.empty(); 
```

💡 Useful links
- [`empty()` in docs](https://docs.tact-lang.org/language/ref/cells#sliceempty)
- [`dataEmpty()` in docs](https://docs.tact-lang.org/language/ref/cells#slicedataempty)
- [`refsEmpty()` in docs](https://docs.tact-lang.org/language/ref/cells#slicerefsempty)
- [`emptyCell()` in docs](https://docs.tact-lang.org/language/ref/cells#emptycell)