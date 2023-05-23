# Lab: Arrays

[Take me to the lab!](https://kodekloud.com/topic/lab-arrays/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).

All the code fragments in this lab are complete mini-programs, so you can paste them into the editor and run them to see the results:

<details>
<summary>Running the code fragments</summary>

1. Right click in Explorer pane to create a new file, e.g. `test.go`
1. Paste the question code snippet into the editor pane
1. Open the terminal window and execute `go run test.go`
1. Re-use your `test.go` file by replacing the content with that of the next question.

</details>

### Questions


1.  <details>
    <summary>Select the correct statement(s) for initialising an array.</summary>

    1. `var arr [5]string := [5]string {}`
    1. `var arr [5]string = [5]string {}`
    1. `arr := [5]string {}`
    1. `var arr := […]string {}`

    <details>
    <summary>Reveal</summary>

    > B, C

    We can rule out A and D immediately, since you canot use `:=` in any `var` statement.

    </details>
    </details>

1.  <details>
    <summary>What is the length and capacity of <b>[1, 2, 3, 4]</b></summary>

    * Length = 4, capacity = 6
    * Length = 4, capacity = 10
    * Length = Capacity = 4
    * Length = 4, capacity = 3

    <details>
    <summary>Reveal</summary>

    > Length = Capacity = 4

    With no further information about how the list was allocated, then we can assume that both length and capacity are equal to the number of elements in the list.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            arr := [...]string{1, 2, 3, 4, 5}
            fmt.Println(arr)
    }
    ```

    * `[]`
    * Error
    * `[1 2 3 4 5]`
    * `["1", "2", "3", "4", "5"]`

    <details>
    <summary>Reveal</summary>

    > Error

    The program would not compile. You cannot initialize a `string` array with integer values.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            arr := [5]bool{true, true, true, true}
            for i := 0; i < len(arr); i++ {
                    if arr[i] {
                            fmt.Println(i)
                    }
            }
    }
    ```

    * 0<br/>1<br/>2<br/>3
    * 0 1 2 3 4
    * 0<br/>1<br/>2<br/>3<br/>4
    * Error

    <details>
    <summary>Reveal</summary>

    > 0<br/>1<br/>2<br/>3

    * An array large enough for 5 `bool` values has been created.
    * Values of `true` have been provided for the first 4 array elements - this means that the remaining one element in the array (`arr[4]`) will have the default value for `bool` which is `false`. So the array looks like this

        | 0    | 1    | 2    | 3    | 4     |
        |------|------|------|------|-------|
        | true | true | true | true | false |

    * The `for` loop will iterate across all five values in the array, counting from zero to 4 inclusive.
    * Since `arr[4]` contains `false`, only numbers as far as 3 will be printed.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            arr := [5]bool{true, true}
            fmt.Println(arr)
    }
    ```

    * [true true false false true]
    * [true true]
    * [true true false false false]
    * [true true true true true]

    <details>
    <summary>Reveal</summary>

    > [true true false false false]

    Again, this is about knowing that the default value of the array's type will be used to intialize the elements of the array for which explict values have not been provded. This is a 5 element array, and values have only been provided for the first two elements. It looks like this:

    | 0    | 1    | 2     | 3     | 4     |
    |------|------|-------|-------|-------|
    | true | true | false | false | false |


    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            arr := [4]int{10, 20, 30, 50, 90}
            fmt.Println(arr)
    }
    ```

    * [10 20 30 40 50
    * [10 20 30 40 0]
    * [10 20 30 40]
    * Error

    <details>
    <summary>Reveal</summary>

    > Error

    * An array large enough for 4 values has been declared.
    * The initializer is passing 5 values. This is an error as the values won't fit, so the program will not compile.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            arr := [10]int{10, 20, 30, 50}
            fmt.Println(arr)
            fmt.Println(len(arr))
    }
    ```

    * [10 20 30 50]
    * [10 20 30 50 0 0 0 0 0 0]<br/>4
    * [10 20 30 50 0 0 0 0 0 0]<br/>10
    * [10 20 30 50]<br/>10

    <details>
    <summary>Reveal</summary>

    > [10 20 30 50 0 0 0 0 0 0]<br/>10

    * The array has been declared to have 10 elements - this means `len(arr)` is 10.
    * It has been initialized with 4 values, therefore the remaining 6 values will have the default value for `int` which is zero. It looks like this

        | 0  | 1  | 2  | 3  | 4 | 5 | 6 | 7 | 8 | 9 |
        |----|----|----|----|---|---|---|---|---|---|
        | 10 | 20 | 30 | 50 | 0 | 0 | 0 | 0 | 0 | 0 |


    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            arr := [10]int{10, 20, 30, 50}
            fmt.Println(arr[0])
            fmt.Println(arr[2])
            fmt.Println(arr[4])
            fmt.Println(arr[8])
            fmt.Println(arr[10])
    }
    ```

    * Error
    * 10 30 0 0 0<br/>10
    * 10<br/>30<br/>0<br/>0<br/>nil
    * 10<br/>30<br/>0<br/>0<br/>0

    <details>
    <summary>Reveal</summary>

    > Error

    * Remember that array indexes start at zero, not 1.
    * The array has been declared to have 10 elements. These will be `arr[0]` thru `arr[9]`
    * `arr[10]` is trying to access the 11th element which doesn't exist, therefore the program will not compile.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            arr := [5]string{"a", "b", "c"}
            for index, element := range arr {
                    fmt.Println(index, "->", element)
            }
    }
    ```

    * 0 -> a<br/>1 -> b<br/>2 -> c<br/>3 -> d<br/>4 -> e
    * 0 -> a<br/>1 -> b<br/>2 -> c<br/>3 -><br/>4 ->
    * 0 -> a<br/>1 -> b<br/>2 -> c<br/>3 -> 3<br/>4 -> 4
    * Error

    <details>
    <summary>Reveal</summary>

    > 0 -> a<br/>1 -> b<br/>2 -> c<br/>3 -><br/>4 ->

    * We have a 5 element string array, for which only the first 3 values have been initialized. The remaining 2 values will have the default value for `string`, which is an empty string (`""`) It looks like this

        | 0 | 1 | 2 | 3 | 4 |
        |---|---|---|---|---|
        | a | b | c |   |   |

    * The range keyword returns the index and value for each element in the array.
    * Thus 3 and 4 print as they do, because their values are empty.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            arr := [5][2]string{{"a"}, {"b"}, {"c"}}
            fmt.Println(arr[0][0])
            fmt.Println(arr[1][1])
            fmt.Println(arr[2][0])
    }
    ```

    * a<br/><br/>c
    * a<br/>b<br/>c
    * a<br/>c<br/><br/>
    * Error

    <details>
    <summary>Reveal</summary>

    > a<br/><br/>c

    Here we have a two dimensional array, 5 wide and 2 deep. And there are default values everywhere! Let's visualize this data structure. It's like an Excel spreadsheet!

    |   | 0 | 1 | 2 | 3 | 4 |
    |---|---|---|---|---|---|
    | 0 | a | b | c |   |   |
    | 1 |   |   |   |   |   |

    Given `arr[x][y]`, look up `x` as the column number and `y` as the row number.

    Thus `arr[0][0]` is `a`, `arr[1][1]` is empty, `arr[2][0]` is `c`.

    </details>
    </details>

