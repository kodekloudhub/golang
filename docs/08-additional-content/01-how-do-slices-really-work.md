# Bonus: How do slices *really* work?

Now that you have reached the end of the course and learned about arrays, slices, structs and pointers, we can take a deep dive into the mechanics of what makes a slice work under the hood. Hopefully this covers all the questions raised on the KodeKloud forums about slices.

In some of the code examples below, it is stated "pseudo-code". For those that haven't come across this term, pseudo-code shows a description of the logic that would happen in the *real* code, some of which in these cases would have been written in assembly language rather than pure Go in the Go runtime, for speed."pseudo-function" indicates a made up function call representative of what is actually happening under the hood. Don't try running any of the pseudo-code, it won't work! It serves only as an illustration. Any example complete with `package` and `import` will run.

* [Refresher](#refresher)
* [Slice Representation](#slice-representation)
* [Slicing arrays and other slices](#slicing-arrays-and-other-slices)
* [Growing Slices](#growing-slices)

## Refresher

You've learned that an array is passed by value. This means that if you pass an array as a function argument, changing the array from inside the function has no effect on the caller's array, since the function gets a complete copy of the *entire* array...

```go
package main

import "fmt"

func modify([3]int arr) {
    arr[0] = 100
}

func main() {
    arr:= [3]int{1, 2, 3}
    modify(arr)
    fmt.Println(arr)
}
```

This yields

```
[1 2 3]
```

You've also learned that a slice is passed "by reference" (in quotes for reasons that will become clear shortly!). This means that if you pass the slice as a function parameter then changing the slice from inside the function *does* affect the caller's slice (most of the time :smile: - we will see when this is *not* the case later)...

```go
package main

import "fmt"

func modify([]int arr) {
    arr[0] = 100
}

func main() {
    arr:= []int{1, 2, 3}
    modify(arr)
    fmt.Println(arr)
}
```

This yields

```
[100 2 3]
```

# Slice Representation

Well... slices are not in reality passed by reference. In fact, they too are passed by value!

The internal representation of a slice is this struct (also called a slice header), and it is an instance of this struct that is passed to a function call that has a slice argument:

```go
type slice struct {
	array unsafe.Pointer    // Pointer to the first element in the slice.
	len   int               // Length of the slice
	cap   int               // Capacity of the slice
}
```

So, the reason a slice argument acts as though passed by reference is the pointer member of the above struct. Even though the slice header is passed by value (meaning *a copy* of the slice header is received by the `modify` function), the pointer `array` is still the same value, meaning it is pointing to the *same* block of memory that `main` is seeing. Thus when you modify a value in the slice, the caller will see the modification.

A note about `unsafe` - The `unsafe` package contains methods and types that circumvent the type safety of Go, so should be used with caution! In the `slice` struct above, `unsafe.Pointer` is used because it can point to *anything* - `int`, `string`, `float32`, an instance of your custom struct - literally anything.

Now let's talk a little more on the functions we can use with slices, with respect to what we have just learned about the representation of a slice using some pseudo-code.

The function `len()` when used with slices is effectively this:

```go
func len(sh slice) {
    return sh.len
}
```

Similarly `cap()`:

```go
func cap(sh slice) {
    return sh.cap
}
```

And `make` is a bit like this. The compiler automatically adjusts the `make` call for the type being stored in the slice, so for `[]int` it would be similar to

```go
func make([]int, lenAndCap ...int) slice {
    length = lenAndCap[0]
    if len(lenAndCap) > 1 {
        capacity = lenAndCap[1]
    } else {
        capacity = length
    }

    return slice {
        array: alloc(capacity * sizeof(int)),
        len:   length,
        cap:   capacity,
    }
}
```

For a custom struct

```go

type myStruct struct {
    a int
    b int
}

func make([]myStruct, lenAndCap ...int) slice {
    length = lenAndCap[0]
    if len(lenAndCap) > 1 {
        capacity = lenAndCap[1]
    } else {
        capacity = length
    }

    return slice {
        array: alloc(capacity * sizeof(myStruct)),
        len:   length,
        cap:   capacity,
    }
}
```

In the above, note:

* The pseudo-function `sizeof` determines how many bytes are required to store a single element of the type contained in the slice e.g. `int`, which on modern computers is 8 bytes. Multiply that by the requested capacity to get the total number of bytes required to hold the slice.
* The pseudo-function `alloc` allocates the requested number of bytes of memory from the global heap and returns a pointer to that memory.

You can see a slice header like this

```go
package main

import (
    "fmt"
    "reflect"
    "unsafe"
)

func main() {
    slc := []int{1, 2, 3}
    sh := (*reflect.slice)(unsafe.Pointer(&slc))
    fmt.Printf("%+v", sh)
}
```

Output will be something like this

```
&{array:1792106 len:3 cap:3}
```

## Slicing arrays and other slices

Recall that when we create a slice over an array or another slice, we are effectively creating a view of a portion of the underlying slice or array.

```go
package main

import "fmt"

func main() {
	arr := [3]int{1, 2, 3}
	slc := arr[:]
	slc[0] = 100
	fmt.Println(arr)
}
```

Output will be

```
[100 2 3]
```

...because we modified the underlying array through the slice. If we look at the assignment `slc := arr[:]`, the compiler generates something like this pseudo-code, then compiles it. The numbers either side of `:` in `[:]` represent the start and end indices of the underlying array or slice to create the view from. Let's assume the compiler automatically generates `0` for start if there's nothing to the left of `:` and `len(arr)` if there's nothing to the right

For an array:

```go
// Compiler generated makeSlice function
func makeSlice(arr *[3]int, start, end int) []int {
    // Remember "arr" is a pointer to the start of the array data
    return slice {
        array: arr + (start * sizeof(int)), // points to the first element in underlying array as specified by "start"
        len: end - start,
        cap: end - start,
    }
}

func main() {
	arr := [3]int{1, 2, 3}
	slc := makeSlice(&arr, 0, len(arr)) // compiler generated
	slc[0] = 100
	fmt.Println(arr)
}
```

For another slice:

```go
// Compiler generated makeSlice function
func makeSlice(slc []int, start, end int) []int {
    // get slice header for slc
    sh := (*reflect.slice)(unsafe.Pointer(&slc))
    return slice {
        array: sh.array + (start * sizeof(int)), // points to the first element in underlying slice as specified by "start"
        len: end - start,
        cap: end - start,
    }
}

func main() {
	originalSlice := []int{1, 2, 3}
	slc := makeSlice(originalSlice, 0, len(arr)) // compiler generated
	slc[0] = 100
	fmt.Println(originalSlice)
}
```

## Growing Slices

A slice grows when its *capacity* is exceeded by appending more elements than capacity permits. The pseudo-code for `append` looks something like this

```go
func append(slc []typ, appendedItems ...typ) []typ {
    // Intially return the slice passed as an argument
    returnSlice := slc

    if len(appendedItems) + len(slc) > cap(slc) {
        // A new slice is allocated (pseudo-function growSlice)
        returnSlice := growSlice(slc, len(appendedItems) + len(slc))
    }

    // pseudo-function, appends the items to the slice and sets length
    copyNewItems(returnSlice, appendedItems)
    return returnSlice
}
```

Now, if the slice did not grow, then what is returned by `append` is the same slice you passed into `append`. If the slice had to grow, then a *completely new* bigger slice is returned, with a new memory allocation and a copy of the data from the original slice, plus any appended data. The length of this slice is the original length plus the length of the data being append, and the capacity is calculated as discussed further on in this section. This has an effect on what a calling function sees. Let's return to the `modify` example, and this time, force the slice to grow.

```go
package main

import "fmt"

func modify(slc []int) {
    slc2 := []int{4, 5, 6, 7, 8, 9}
    // Grow the slice
    slc = append(slc, slc2...)
    // Now modify first element
    slc[0] = 100
}

func main() {
    slc := []int{1, 2, 3}
    modify(slc)
    fmt.Println(slc)
}
```

This time the output is:

```
[1 2 3]
```

That's because a grow happened in the `modify` function, which caused a *copy* to be made of the original data, so when `slc[0] = 100` happens, it's now modifying a copy, not the original data therefore it's as if we had passed an array and not a slice! This is also why you should always assign the result of `append` back to the slice you are appending to, in case the slice is reallocated.

Next, let's discuss what happens when a slice grows. The general rule of thumb is that the capacity is doubled, but this is not always the case! The algorithm for growing a slice is fairly complex and takes several factors into consideration when deciding how much extra capacity should be added. One such consideration is that when the slices get to a certain size, the capacity increase factor drops from 2 to 1.25 or you would soon run out of memory! There are other considerations for the size of the element stored in the slice, and the machine architecture. The code for growing a slice can be [found here](https://go.dev/src/runtime/slice.go) beginning at line 157.

