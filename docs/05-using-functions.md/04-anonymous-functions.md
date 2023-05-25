# Lab: Anonymous Functions

[Take me to the lab!](https://kodekloud.com/topic/lab-anonymous-functions/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).


1.  <details>
    <summary>What is the most appropriate definition for recursion?</summary>

    1.  ```go
        var my_func := (func(s string) {fmt.Println("Hey there,", s)})
        ```
    1.  ```go
        var (my_func = func(s string) {fmt.Println("Hey there,", s)})
        ```
    1.  ```go
        func main() {
            var (
                    my_func = func(s string) { fmt.Println("Hey there,", s) }
            )
            my_func("Joe")
        }
        ```
    1.  ```go
        var my_func func := (func(s string) {fmt.Println("Hey there,", s)})
        ```

    <details>
    <summary>Reveal</summary>

    > B, C

    Quite simply, you can never use `:=` with a `var` statement, leaving only two possible answers.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import (
            "fmt"
            "strings"
    )

    func main() {
            x := func(s string) string {
                    return strings.ToUpper(s)
            }
            fmt.Printf("%T \n", x)
            fmt.Println(x("Joe"))
    }
    ```

    * func(string) string<br/>joe
    * func(string) string<br/>JOE
    * string<br/>Joe
    * func(string)<br/>JOE

    <details>
    <summary>Reveal</summary>

    > func(string) string<br/>JOE

    * Declare a variable `x` as an anonymous function that takes a `string`, returns a `string` with a body that returns the uppercase of what ever is passed as the argument.
    * Print the type of variable `x`, which will yield the function signature. A signature comprises:
        1. `func`
        1. `(`
        1. List of argument *types* (if any)
        1. `)`
        1. Return type(s) (if any) - the return types being a bracketed list if there is more then one.
    * Print the invocation of the function via `x`, passing "Joe" as an argument. This is returned as "JOE" which gets printed.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import (
        "fmt"
        "strings"
    )

    func main() {
        x := func(s string) {
            fmt.Println(strings.ToLower(s))
        }
        fmt.Printf("%T \n", x)
        x("RacheL")
    }
    ```

    * func(string)<br/>rachel
    * func(string) string<br/>RACHEL
    * func(string) string<br/>rachel
    * func(string)<br/>Rachel

    <details>
    <summary>Reveal</summary>

    > func(string)<br/>rachel

    Very similar to the previous question, however

    * Variable `x` is assigned the anonymous function
    * The function handles the printing itself, therefore does not return anything, thus the signature that is printed is only `func(string)`
    * The function is lowercasing the value it is given.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import (
        "fmt"
        "strings"
    )

    func main() {
        x := func(s string) {
            fmt.Println(strings.ToLower(s))
        }("RacheL")
        fmt.Printf("%T \n", x)
    }
    ```

    * func(string)<br/>Rachel
    * Error
    * func(string) string<br/>rachel
    * func(string)<br/>rachel

    <details>
    <summary>Reveal</summary>

    > Error

    * The compiler detects an attempt to call the function during assignment of an anonymous function to a variable :- `}("RacheL)`. This is illegal so the program fails to compile.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    Add package and import statements as needed

    ```go
    var (
            cube = func(i int) string {
                    c := i * i * i
                    return strconv.Itoa(c)
            }
    )

    func main() {
            x := cube(8)
            fmt.Printf("%T %v", x, x)
    }
    ```

    * func(i int) string<br/>512
    * int 512
    * func(i int) int string<br/>512
    * string 512

    <details>
    <summary>Reveal</summary>

    > string 512

    Note the use of `strconv.Itoa`. To build this program requires the additional import of `"strconv"`. Recall from earlier labs that `Itoa` converts an integer to its string representation.

    * `cube` is declared as a package variable that holds an anonymous function that takes `int` and returns `string`
    * The function computes the cube of `i`, converts that to a string and returns it.
    * In `main()` variable `x` is assigned the value returned by calling `cube` with 8.
    * Finally print the type and value of `x`. `x` is the value returned by `cube`, not `cube` itself, therefore its type is `string`. The value of `x` is the string "512" so that's just printed. It's all on the same line since it's a single `Printf` with no newline character in it.

    </details>
    </details>

