# Lab: Function Syntax

[Take me to the lab!](https://kodekloud.com/topic/lab-function-syntax/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).

1.  <details>
    <summary>Define a function with following specs, and choose the correct definition</summary>

    * Name of function: `returnCube`
    * Input parameters: `int`
    * Output parameters: `int`
    * The function calculates the cube of `n` (`n*n*n`)

    Is it -

    *   ```
        func returnCube(n) int {
            return n*n*n
        }
        ```
    *   ```
        func returnCube(int) int {
            return n*n*n
        }
        ```
    *   ```
        func returnCube(n int) int {
            return n*n*n
        }
        ```
    *   ```
        funct returnCube(n int) int {
            return n*n*n
        }
        ```


    <details>
    <summary>Reveal</summary>

    ```
    func returnCube(n int) int {
        return n*n*n
    }
    ```

    Function syntax is as follows

    1. keyword `func` (not `funct`)
    1. input parameters surrounded with brackets `()`, or empty brackets if no input parameters.
    1. Each input parameter is variable name followed by type, e.g. `n int`.
    1. After `)` is the *type* of what we want to return (if anything), in this case `int`
    1. Lastly `{` to begin the function body.

    Then we have the code of the function followed by `}` to close it off
    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:  (add package declarations and import statements as needed)</summary>

    ```go
    func returnCube(n int) int {
            return n*n*n
    }

    func main() {
            returnCube(5)
    }
    ```

    * no output
    * error
    * 5 125
    * 125

    <details>
    <summary>Reveal</summary>

    > no output

    Why? Becuase we are not doing anything with the value we get from `returnCube`, certainly not printing it!

    Note that to try this program, you would have to include `package main` as the first line.

    </details>
    </details>

1.  <details>
    <summary>Select valid function declarations from the below options.</summary>

    1. `func 3doSomething(n int) int`
    1. `func doSomething(a int, b int) int`
    1. `func doSomething(n int) int`
    1. `func do Something(n int) int`

    <details>
    <summary>Reveal</summary>

    > B. C

    * A is incorrect because an identifier (function name, variable name etc.) cannot start with a digit.
    * D is incorrect because an identifier cannot contain whitespace.

    </details>
    </details>

1.  <details>
    <summary>Choose the correct function declaration of function <b>printDetails</b> so the following code can be executed successfully in main function.</summary>

    ```go
    var s string
    s = printDetails("Joe")
    fmt.Print(s)
    ```
    and gives the following output

    ```
    Joe
    1
    ```

    * `func printDetails(s string) int`
    * `func print_Details(s string) string`
    * `func printDetails(s int) string`
    * `func printDetails(s string) string`

    <details>
    <summary>Reveal</summary>

    > `func printDetails(s string) string`

    To answer this, you do not need to be concerned about the actual output other then realizing that it must be a string. What you do need to be concerned about is selecting the correct function *signature* from the four options.

    * `func printDetails(s string) int` - is incorrect as it returns an `int`. Not possible to get the required output with an int return type.
    * `func print_Details(s string) string` - is incorrect because the function is named incorrectly.
    * `func printDetails(s int) string` - returns the correct type, but is incorrect because its input is `int` - can't pass `Joe` as an int parameter.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    func printDetails(s string) {
            fmt.Println(s)
    }

    func main() {
            x := printDetails("Joe")
            fmt.Print(x)
    }
    ```

    * error
    * empty string
    * nil
    * 0

    <details>
    <summary>Reveal</summary>

    > error

    The program will not compile due to this

    `x := printDetails("Joe")`

    Look at `printDetails` function. Does it return anything? No, so you can't assign a variable from the result of a call to this function.

    </details>
    </details>

