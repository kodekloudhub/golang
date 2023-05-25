# Lab: Functions

[Take me to the lab!](https://kodekloud.com/topic/lab-functions-2/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).


1.  <details>
    <summary>Select the correct statement(s) for defer statement.</summary>

    1. `defer` statement delays the execution of a function until the previous function returns.
    1. `defer` statement delays the execution of a function until the following function returns.
    1. `defer` statement delays the execution of a surrounding function until the current function returns.
    1. `defer` statement delays the execution of a function until the surrounding function returns.

    <details>
    <summary>Reveal</summary>

    > D

    ```go
    func afunction() {
        // This function is surrounding the folliowing defer
        defer fmt.Println("defer executed")
        fmt.Println("this will print first")
    } // defer executes here
    ```

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program?</summary>

    ```go
    package main

    import "fmt"

    func printString(str string) {
        fmt.Printf("%q ", str)
    }

    func printInt(i int) {
        fmt.Printf("%d ", i)
    }

    func printFloat(f float64) {
        fmt.Printf("%.2f ", f)
    }
    func main() {
        printString("browser")
        defer printInt(32)
        defer printFloat(0.24)
        printString("chrome")
        printInt(90)
        defer printFloat(89)
        printInt(900)
    }
    ```

    * "browser" "chrome" 90 0.24 32 900 89.00
    * browser chrome 90 900 89.00 0.24 32
    * "browser" "chrome" 90 900 89.00 0.24 32
    * browser chrome 0.24 32 90 900 89.00

    <details>
    <summary>Reveal</summary>

    > "browser" "chrome" 90 900 89.00 0.24 32

    * `printString` uses the `%q` formatter meaning that strings are printed in quotes. This rules out two possible answers.
    * Recall that `defer` statements execute after everything else in the function, so this means that "browser", "chrome" and 90 will be output first.
    * Recall that multiple `defer` statements execute in the reverse order to which they are declared. This a "stack" behaviour: last in first out. This tells us that the order of output from the defers will be 89.00, 0.24, 32 - yielding the correct answer.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program?</summary>

    ```go
    package main

    import (
        "fmt"
        "strings"
    )

    func getString(str string) (string, string) {
        return strings.ToLower(str), strings.ToUpper(str)
    }

    func main() {
        _, lower := getString("BROWSER")
        fmt.Println(lower)
    }
    ```

    * browser
    * error
    * BROWSER
    * Browser

    <details>
    <summary>Reveal</summary>

    > BROWSER

    * The function `getString` returns two values:
        1. Lower case version of the input
        2. Upper case version of the input
    * When the function is called in `main`, the assignment is to `_, lower`.
    * The first return value (the lowercase version) is discarded (assigned to `_`).
    * The second return value (the uppercase version) is assigned to `lower`, which is then printed.

    </details>
    </details>

1.  <details>
    <summary>Make the required changes in the function body:</summary>

    ```go
    func greetings() (x, y string) {
        x := "hello "
        y := "world"
    }

    func main() {
        fmt.Print(greetings())
    }
    ```

    ...so the output is `hello world`. Select the corect definitions:

    1.  ```go
        func greetings() (x, y string) {
                x := "hello "
                y := "world"
            return x, y
        }
        ```
    1.  ```go
        func greetings() (x, y string) {
            x = "hello "
            y = "world"
            return x, y
        }
        ```
    1.  ```go
        func greetings() (x, y string) {
            x = "hello "
            y = "world"
            return
        }
        ```
    1.  ```go
        func greetings() (x, y string) {
                x := "hello "
                y := "world"
            return "hello world"
        }
        ```

    <details>
    <summary>Reveal</summary>

    > B, C

    * A is incorrect because `x` and `y` are named return values, therefore they cannot be reassigned with `:=`
    * B is correct because the values are correctly assigned. You can return the named variables by name.
    * C is correct because the values are correctly assigned, and the named variables are implicitly returned.
    * D is incorrect for the same reason as A, and also because it only returns one value when two are expected.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program?</summary>

    ```go
    package main

    import (
        "fmt"
    )

    func main() {
        fmt.Println(f1())
    }

    func f1() int {
        return f2()
    }

    func f2() int {
        return 1
    }
    ```

    * 1 1
    * no output
    * error
    * 1

    <details>
    <summary>Reveal</summary>

    > 1

    Starting from `main`
    1. It prints the return value of `f1()`
    1. `f1` returns the function `f2`
    1. `f2` returns `1`

    Thus the `fmt.Println` is actually calling `f2` as it's what is returned by `f1`.

    </details>
    </details>

