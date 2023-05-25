# Lab: High Order Function

[Take me to the lab!](https://kodekloud.com/topic/lab-high-order-functions/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).

1.  <details>
    <summary>Select the correct statement(s) for high order functions</summary>

    1. Function that receives a function as an argument.
    1. Function that contains a function.
    1. Function that returns another function.
    1. Function that calls another function.

    <details>
    <summary>Reveal</summary>

    > A. C

    These two answers correctly define a high order function.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program?</summary>

    ```go
    package main

    import "fmt"

    func addHundred(x int) int {
        return x + 100
    }
    func partialSum(x ...int) func() {
        sum := 0
        for _, value := range x {
            sum += value
        }
        return func() {
            fmt.Println(addHundred(sum))
        }
    }
    func main() {
        partial := partialSum(1, 2, 3, 4, 5)
        partial()
    }
    ```

    * 110
    * 15
    * Error
    * 115

    <details>
    <summary>Reveal</summary>

    > 115

    * The function `partialSum` adds together the values of the integers it receives and stores them in `sum`.
    * It then returns an anonymous function that prints the value of `sum` plus 100 (via call to `addHundred`).
    * Recall that the body of this anonymous function is an inner scope with respect to `partialSum` meaning it can use the variable `sum`.
    * The variable `partial` is assigned the result of the call to `partialSum`. Its value is the anonymous function returned by `partialSum`.
    * Finally the anonymous function is executed via the variable `partial` by applying the call operator `()` - i.e. `partial()` and the result is printed.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program?</summary>

    ```go
    package main

    func addHundred(x int) int {
        return x + 100
    }
    func partialSum(x ...int) func() int {
        sum := 0
        for _, value := range x {
            sum += value
        }
        return func() int {
            return addHundred(sum)
        }
    }
    func main() {
        partial := partialSum(1, 2, 3)
        partial()
    }
    ```

    * 106
    * no output
    * Error
    * 115

    <details>
    <summary>Reveal</summary>

    > No output

    Quite simply there is no `fmt.Println` so nothing will be printed.

    This is a minor variation on the previous question. The caculated result would indeed be `106`, but since the `fmt.Println` has been removed from the returned anonymous function, there is no output.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program?</summary>

    ```go
    package main

    import "fmt"

    func addHundred(x int) int {
        return x + 100
    }
    func partialSum(add100 func(x int) int, x ...int) int {
        sum := 0
        for _, value := range x {
            sum += value
        }
        return add100(sum)

    }
    func main() {
        partial := partialSum(addHundred, 1, 2, 3)
        fmt.Println(partial)
    }
    ```

    * 6
    * 115
    * 106
    * error

    <details>
    <summary>Reveal</summary>

    > 106

    Yet another variation on the theme, however this time...

    * The `addHundred` function is being passed as the first argument to `partialSum`, then the list of integers to sum.
    * `partialSum` sums the integers, then calls the `addHundred` function and returns its result.
    * `main()` assigns that value to `partial` (whose type will now be `int`), and prints it.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program?</summary>

    ```go
    package main

    import "fmt"

    func addHundred(x int) {
        fmt.Println(x + 100)
    }
    func partialSum(add100 func(x int), x ...int) int {
        sum := 0
        for _, value := range x {
            sum += value
        }
        add100(sum)
        return 0
    }
    func main() {
        partial := partialSum(addHundred, 1, 2, 3)
        fmt.Println(partial)
    }
    ```

    * Error
    * 106<br/>0
    * 115<br/>1
    * 115<br/>0

    <details>
    <summary>Reveal</summary>

    > 106<br/>0

    Similar to the previous question, however this time...

    * `addHundred` does the printing of the result of the sum.
    * `partialSum` simply returns zero
    * `main()` assigns that value to `partial` (whose type will now be `int`), and prints it (zero).

    </details>
    </details>


