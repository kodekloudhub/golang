# Lab: Slices

[Take me to the lab!](https://kodekloud.com/topic/lab-slices/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).

All the code fragments in this lab are complete mini-programs, so you can paste them into the editor and run them to see the results:

<details>
<summary>Running the code fragments</summary>

1. Right click in Explorer pane to create a new file, e.g. `test.go`
1. Paste the question code snippet into the editor pane
1. Open the terminal window and execute `go run test.go`
1. Re-use your `test.go` file by replacing the content with that of the next question.

</details>

Before we start, a frequently asked question on Slack and the forums is about slice capacity when a slice grows: "I thought that the capacity always doubles when a slice grows". The answer to that is *usually*, not *always*. It depends on the length of the intial slice, how much data is being appended, and how big the capacity is at the time it is grown. If it always doubled, you could run out of memory very quickly! The code for growing a slice is [here](https://github.com/golang/go/blob/master/src/runtime/slice.go#L157), but it's very complicated!

### Questions

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            arr := []int{-1, -2}
            for _, value := range arr {
                    fmt.Println(value)
            }
    }
    ```

    * -1<br/>-2<br/>0<br/>0<br/>0
    * -1<br/>-2
    * [-1, -2]
    * [-1 -2]

    <details>
    <summary>Reveal</summary>

    > -1<br/>-2

    * Know that slices are variable length arrays. When you declare a slice with initial values as has been done in this program, its length is equal to the number of values it was initialized with, so that rules out more than 2 values being printed.
    * The `Println` is printing individual values, not the whole slice, so that eliminates anything with `[]`

    </details>
    </details>

1.  <details>
    <summary>What would be the length and capacity of the slice here.</summary>

    ```go
    arr := [5]string{"a", "b", "c", "d", "e"}
    slice := arr[:4]
    ```

    * Length: 5, Capacity: 5
    * Length: 4, Capacity: 5
    * Length: 5, Capacity: 4
    * Length: 4, Capacity: 4

    <details>
    <summary>Reveal</summary>

    > Length: 4, Capacity: 5

    * `arr[:4]` creates a new *slice* using the first 4 elements of `arr`. `arr` can be an array (as it is here), or another slice.
    * The length of the new slice is equal to the number of elements copied. The capacity is equal to the capacity of `arr`. For arrays (like `arr`), capacity is always equal to length.
    * Importantly, the new slice is actually a "view" of the source data. A copy is not made of the original array; the slice is referencing the same memory as the original array, and is why the capacities are equal - as will be seen in the next question!

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            arr := [5]string{"a", "b", "c", "d", "e"}
            slice := arr[:4]
            fmt.Println(arr)
            fmt.Println(slice)
            slice[1] = "x"
            fmt.Println(arr)
            fmt.Println(slice)
    }
    ```

    * [a b c d e]<br/>[a b c d]<br/>[a b c d e]<br/>[a x c d]
    * [a b c d e]<br/>[b c d]<br/>[a x c d e]<br/>[x c d]
    * [a b c d e]<br/>[a b c d]<br/>[a x c d e]<br/>[a x c d]
    * [a b c d e]<br/>[a b c d]<br/>[a b x d e]<br/>[a b x d]

    <details>
    <summary>Reveal</summary>

    > [a b c d e]<br/>[a b c d]<br/>[a x c d e]<br/>[a x c d]

    * The first two `Println` are showing the contents of `arr` and `slice`
    * Now we set the second element of `slice` to be `x`.
    * Print the array and the slice again - but wait! The second value in the array has also been updated! Why? This is due to the explanation given in the last question.

    </details>
    </details>

1.  <details>
    <summary>Follow the given steps, and select the correct output</summary>

    1. create an integer array of size 5 with values [10, 20, 90, 70, 60]
    1. create a slice referencing the above array to contain elements from index 0, 1, 2
    1. change the element at index 2 of slice to 900
    1. print the array
    1. print the slice

    Output is?

    * [10 20 900 70 60]<br/>[10 20 900]
    * [10 20 90 70 60]<br/>[10 20 90]
    * [10 20 90 70 60]<br/>[10 20 900 70 60]
    * [10 20 90 70 60]<br/>[10 20 900]

    <details>
    <summary>Reveal</summary>

    > [10 20 900 70 60]<br/>[10 20 900]

    Let's write a program to verify this

    ```go
    package main

    import "fmt"

    func main() {
        // create an integer array of size 5 with values [10, 20, 90, 70, 60]
        arr := [5]int{10, 20, 90, 70, 60}
        // create a slice referencing the above array to contain elements from index 0, 1, 2
        slice := arr[:3]
        // change the element at index 2 of slice to 900
        slice[2] = 900
        // print the array
        fmt.Println(arr)
        // print the slice
        fmt.Println(slice)
    }
    ```

    As in the previous question, the slice is a view of the underlying array so changing a value in the slice also changes the corresponding value in the array.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            arr := [5]int{10, 20, 90, 70, 60}
            slice := arr[:3]
            fmt.Println(cap(slice))
            new_slice := append(slice, 100, 200)
            fmt.Println(cap(new_slice))
    }
    ```

    * 5<br/>5
    * 5<br/>10
    * 5<br/>7
    * 10<br/>10

    <details>
    <summary>Reveal</summary>

    > 5<br/>5

    * The capacity of the slice begins as 5 since we are overlaying the `[5]int` array.
    * Appending two more values isn't going to exceed the capacity of 5

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            arr := [5]int{10, 20, 90, 70, 60}
            slice := arr[:3]
            fmt.Println(cap(slice))

            slice_2 := make([]int, 5, 20)
            new_slice := append(slice, slice_2...)
            fmt.Println(cap(new_slice))
    }
    ```

    * 5<br/>5
    * 3<br/>23
    * 5<br/>25
    * 5<br/>10

    <details>
    <summary>Reveal</summary>

    > 5<br/>10

    1. `slice` has a length of 3 and a capacity of 5
    2. We create a new slice of length 5 and capacty 20, then append it to `slice`
    3. Now the length and capacity of `slice` are exceeded so the runtime reallocates a new slice and copies any data from the original slice to it.
    4. The length of the new slice is the sum of the `len()` of `slice` and `slice_2`: 3 + 5 = 8.
    5. The capacity therefore needs to be increased, and a capacity increase is *usually* a doubling: 5 * 2 = 10
    6. The capacity of `slice_2` is not considered by the slice reallocation code.


    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            arr := [5]int{10, 20, 90, 70, 60}
            slice := append(arr[:2], arr[3:])
            fmt.Println(slice)
    }
    ```

    * Error
    * [10 20 90 70 60]
    * [10 90 70 60]
    * [10, 20, 70, 60]

    <details>
    <summary>Reveal</summary>

    > Error

    You might think the the output shuld be `[10 90 70 60]`. It would be if there wasn't a syntax error in the code. To append a slice to a slice, it requires the `...` syntax, as in the previous question.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            arr := []int{10, 20, 90, 70, 60}
            slice := make([]int, 10)
            num := copy(slice, arr)
            fmt.Println(slice)
            fmt.Println(num)
    }
    ```

    * [10 20 90 70 60 0 0 0 0 0]<br/>10
    * [10 20 90 70 60]<br/>5
    * [10 20 90 70 60 0 0 0 0 0]<br/>5
    * Error

    <details>
    <summary>Reveal</summary>

    > [10 20 90 70 60 0 0 0 0 0]<br/>5

    * We start with an array of length 5
    * We allocate a slice with length 10
    * We then copy the array into the slice and collect the number of items copied in `n`
    * 5 items were copied from `arr` into `slice`, which went into the first 5 elements of `slice`. `slice`'s length is still 10, so those elements contain the default value of `int` - zero.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            arr := []int{10, 20, 90, 70, 60}
            slice := make([]int, 10)
            copy(slice, arr)
            slice[1] = 1000
            fmt.Println(arr)
            fmt.Println(slice)
    }
    ```

    * [10 20 90 70 60]<br/>[10 1000 90 70 60]
    * [10 1000 90 70 60]<br/>[10 1000 90 70 60 0 0 0 0 0]
    * [10 1000 90 70 60 0 0 0 0 0]<br/>[10 1000 90 70 60 0 0 0 0 0]
    * [10 20 90 70 60]<br/>[10 1000 90 70 60 0 0 0 0 0]

    <details>
    <summary>Reveal</summary>

    > [10 20 90 70 60]<br/>[10 1000 90 70 60 0 0 0 0 0]

    * As with the previous question we create an array, a slice and copy the array into the slice.
    * Set the second element of the slice to 1000, then print the array and the slice.
    * Because we created a *new* slice with `make`, it is completely unrelated to the array, so setting a value in the slice has no effect on the array.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            arr := [10]int{10, 20}
            slice := arr[2:8]
            fmt.Println(len(slice))
            fmt.Println(cap(slice))
    }
    ```

    * 10<br/>10
    * 6<br/>8
    * 6<br/>10
    * 6<br/>6

    <details>
    <summary>Reveal</summary>

    > 6<br/>8

    * Make a 10 element array with the first two elements set to 10 and 20 (the remaining 8 will be zero)
    * Make a slice over the array starting at index 2 for 6 elements (start at element 2, up to but not including element 8).
    * `len(slice)` is 6 because we included 6 elements
    * `cap(slice)` is 8 because the slice shares the same memory as the array. The capacity is calculated as length of the array `arr` (10) minus the start index of the slice (2), therefore 8.

    </details>
    </details>

