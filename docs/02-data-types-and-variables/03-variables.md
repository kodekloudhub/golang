# Lab: Variables

[Take me to the lab!](https://kodekloud.com/topic/lab-variables-10/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).

1.  <details>
    <summary>What would be the valid statement for initialising a variable:</summary>

    Note that these answers may be in a different order each time you load the lab.

    * `var name = "Lia"`
    * `var name string = "Lia"`
    * `var string name = "Lia"`
    * `var string name = 98.00`

    <details>
    <summary>Reveal</summary>

    >  `var name string = "Lia"`

    All others are syntax errors.

    </details>
    </details>

1.  <details>
    <summary>Select all the correct statements for variable initialisation</summary>

    1. `var name string = "Lia"`
    1. `name := "Lia"`
    1. `var s, t string = "Lia", "Harry"`
    1. `var b bool = "false"`

    <details>
    <summary>Reveal</summary>

    > A, B, C

    The final decalration is incorrect because `"false"` is a string, not a boolean.

    </details>
    </details>

1.  <details>
    <summary>Select the statements that would print and then introduce a new line in the output:</summary>

    1. `fmt.Print(name)`
    1. `fmt.Print("Hey there \n")`
    1. `fmt.Println("Hey there")`
    1. `fmt.Printf(name)`

    <details>
    <summary>Reveal</summary>

    > B, C

    Know that `fmt.Print` and `fmt.Printf` do not automatically emit a newline; `fmt.Println` does.

    Despite the above statement, 2 emits a newline because it includes the special character `\n` which is the newline character.

    </details>
    </details>

1.  <details>
    <summary>Consider the following code snippet and select the correct output:</summary>

    For this, make use of the code editor. Create a new file e.g. `test.go`. Right click in explorer window to create the file, then paste the given code block into it.

    Run this code from the integrated terminal, and observe the output to find the answer.

    ```
    go run test.go
    ```

    <details>
    <summary>Reveal</summary>

    > D

    Understand what the format specifiers are doing in the `Printf` statements, and what was learned in the previous question:

    * `%.2f` is printing radius to 2 decimal places.
    * `%.1f` is printing PI to 1 decimal place.
    * `%f` is printing area to maximum precision of `float64`. Since the answer is exact at 8 significant figures, that is what's printed.
    * There is no newline before `Thank You` because the previous `fmt.Printf` did not emit one.

    </details>
    </details>

1.  <details>
    <summary>What is the correct format specifier for printing a string with quotes</summary>

    Note that these answers may be in a different order each time you load the lab.

    * `%v`
    * `%s`
    * `%q`
    * `%vv`

    <details>
    <summary>Reveal</summary>

    > `%q`

    `%s` also prints strings, but does not include quotes.

    </details>
    </details>

1.  <details>
    <summary>Among the following code snippets - select the correct ways of initializing variables</summary>

    1.  ```go
        var name := "Priyanka"
        ```

    1.  ```go
        var s,t string,int = "Priyanka", 100
        ```

    1.  ```go
        var (
            s string = "Priyanka"
            i int = 100
        )
        ```

    1.  ```go
        var i,j int = 100, 200
        ```

    <details>
    <summary>Reveal</summary>

    > C, D

    * You can't use `:=` in a `var` declaration
    * You can't declare two separate types in a single line `var` declaration

    </details>
    </details>

1.  <details>
    <summary>Select the correct statement...</summary>

    1. Inner blocks can access variables of outer blocks.
    1. Outer blocks can access variables within inner blocks.
    1. Outer blocks cannot access variables within inner blocks.
    1. Inner blocks can not access variables of outer blocks.


    <details>
    <summary>Reveal</summary>

    > A, C

    </details>
    </details>

1.  <details>
    <summary>From the following code snippet, identify the local and global variable</summary>

    ```go
    package main

    var a string = "foo"

    func main() {
        var b string = "bar"
        {
            var c string = "loreum"
        }
    }
    ```

    1. `a`, `b` - global, `c` - local
    1. `a`, `b`, `c` - local
    1. `a`, `b`, `c` - global
    1. `a` - global, `b`, `c` - local

    <details>
    <summary>Reveal</summary>

    > D

    Global variables are defined with `var` statements outside of any `func`.

    </details>
    </details>

1.  <details>
    <summary>From the following code snippet - which line will cause error</summary>

    ```go
    1. package main
    2.
    3. import "fmt"
    4.
    5. var a string = "foo"
    6.
    7. func main() {
    8.    var b string = "bar"
    9.    fmt.Println(a)
    10.   fmt.Println(b)
    11.   fmt.Println(c)
    12.  {
    13.       var c string = "loreum"
    14.       fmt.Println(a)
    15.       fmt.Println(b)
    16.       fmt.Println(c)
    17.  }
    18. }
    ```
    <details>
    <summary>Reveal</summary>

    > Line 11

    Variable `c` is declared in an inner block. Line 11 is trying to use `c` from an outer block, which as we discovered in Q7 is illegal.

    </details>
    </details>

1.  <details>
    <summary>What is the zero value for the following variables</summary>

    ```go
    var name string
    var b bool
    var f float64
    ```

    1.  ```go
        ""
        true
        1.0
        ```
    1.  ```go
        " "
        false
        1.0
        ```
    1.  ```go
        ""
        false
        0.00
        ```
    1.  ```go
        ""
        true
        0.0
        ```
    <details>
    <summary>Reveal</summary>

    > C

    Don't be fooled by the number of decimal places on the zero value - it's still zero and still a `float64` for which the default is zero. That rules out the first two answers.

    The default for a boolean is always `false`, so that rules out the first and last answer.

    The default for a string is not a string containing one space character, so that rules out the second answer.

    This leaves only the third answer.
    </details>
    </details>

