# Lab: Arithmetic Operators

[Take me to the lab!](https://kodekloud.com/topic/lab-arithmetic-operators/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).

See also [Arithmetic Operators](https://go.dev/ref/spec#Arithmetic_operators) in the Go manual.

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
    <summary>What would be the output of the following code -</summary>

    ```go
    package main

    import "fmt"

    func main() {
            var a string = "one"
            var b int = 2
            fmt.Print(a + b)
    }
    ```

    * Error
    * 2one
    * 3
    * one2

    <details>
    <summary>Reveal</summary>

     > Error

    The program would not compile due to strict type checking performed by the compiler. You cannot add `int` with `string`.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following code -</summary>

    ```go
    package main

    import "fmt"

    func main() {
            var a float64 = 5.9
            var b int = 2
            fmt.Print(a + b)
    }
    ```

    * Error
    * 7.9
    * 7
    * 7.0

    <details>
    <summary>Reveal</summary>

    > Error

    The program would not compile due to strict type checking performed by the compiler. Whilst both varaibles are numeric types, the compiler will not do implict type casts. You could fix it with an *explicit* type cast

    ```go
    fmt.Print(a + float64(b))
    ```

    ...then the answer would be 7.9

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following code -</summary>

    ```go
    package main

    import "fmt"

    func main() {
            var a float64 = 5.9
            a++
            fmt.Print(a)
    }
    ```

    * 5
    * 7.0
    * 6
    * 6.9

    <details>
    <summary>Reveal</summary>

    > 6.9

    `++` is the increment operator. It adds 1 to any numeric variable. `a++` is equivalent to `a = a + 1`

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following code -</summary>

    ```go
    package main

    import "fmt"

    func main() {
            var a int = 10
            a--
            fmt.Print(a)
    }
    ```

    * 10
    * 9
    * 11
    * Error

    <details>
    <summary>Reveal</summary>

    > 9

    `--` is the decrement operator. It subtracts 1 from any numeric variable. `a--` is equivalent to `a = a - 1`

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following code -</summary>

    ```go
    package main

    import "fmt"

    func main() {
            var a, b float64 = 24.4, 3.0
            fmt.Println(a / b)
            fmt.Println(int(a) % int(b))
    }
    ```

    * 8.133333333333333<br/>0
    * 9.001333333333333<br/>0
    * 8.00<br/>0.11
    * 8.2<br/>ERROR

    <details>
    <summary>Reveal</summary>

    > 8.133333333333333<br/>0

    The first operation is a straight division of two floats, so it will produce a float result.

    In the second operation, the floats are first casted to ints so the values become `24` and `3`. Then a modulo division is performed `%`. Modulo yields the *remainder* when the value on the left is divided by the value on the right. Remember from elementary level maths - 24 divided by 3 = 8 *remainder 0*.
    </details>
    </details>

