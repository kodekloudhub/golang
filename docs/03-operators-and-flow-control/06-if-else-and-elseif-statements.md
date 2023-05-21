# Lab: if-else and else if statements

[Take me to the lab!](https://kodekloud.com/topic/lab-if-else-and-else-if-statements//)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).

See also [Assignment](https://go.dev/ref/spec#Assignment_statements) in the Go manual.

All the code fragments in this lab are complete mini-programs, so you can paste them into the editor and run them to see the results:

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
    <summary>What would be the output for the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            var a, b string = "kolkata", "Kolkata"
            if a == b {
                    fmt.Println("strings are equal")
            } else {
                    fmt.Println("strings are not equal")
            }
            fmt.Println("thank you!")
    }
    ```

    * strings are equal
    * strings are equal<br/>thank you!
    * Error
    * strings are not equal<br/>thank you!

    <details>
    <summary>Reveal</summary>

    > strings are not equal<br/>thank you!

    Strings are not equal because there is a difference in capitalisation, so the `if` test is `false`, and the `else` block is executed.

    There's no error as the syntax is correct and it will compile.

    `thank you!` is always printed, as it's not inside of an if-else construct.

    </details>
    </details>

1.  <details>
    <summary>What would be the output for the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            var a, b string = "kolkata", "kolkata"
            if a == b {
                    fmt.Println("strings are equal")
            }
            else {
                    fmt.Println("strings are not equal")
            }
            fmt.Println("thank you!")
    }
    ```

    * strings are equal
    * strings are equal<br/>thank you!
    * Error
    * strings are not equal<br/>thank you!

    <details>
    <summary>Reveal</summary>

    > Error

    There is a syntax error in this code, so it will not compile. Go is strict about the placement of braces.

    ```go
            }
            else {
    ```

    should be

    ```go
            } else {
    ```

    </details>
    </details>

1.  <details>
    <summary>What would be the output for the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            var a, b string = "foo", "bar"
            if a+b == "foo" {
                    fmt.Println("foo")
            } else if a+b == "bar" {
                    fmt.Println("bar")
            } else if a+b == "foobar" {
                    fmt.Println("foobar")
            } else {
                    fmt.Println("None matched")
            }
            fmt.Println("thank you!")
    }
    ```

    * foo<br/>thank you!
    * bar<br/>thank you!
    * None matched<br/>thank you!
    * foobar<br/>thank you!


    <details>
    <summary>Reveal</summary>

    > foobar<br/>thank you!

    1. First, evaluate what is `a+b`. Addtion of strings concatenates them, so we get `foobar`
    1. Now look at the if-else if statements. Which one matches `foobar`? This is the branch the program will follow.

    `thank you!` is always printed, as it's not inside of an if-else construct.

    </details>
    </details>

1.  <details>
    <summary>What would be the output for the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            var a, b string = "foo", "bar"
            if a+b == "foo" {
                    fmt.Println("foo")
            } else if a+b == "foobar" {
                    fmt.Println("bar")
            } else if a+b == "foobar" {
                    fmt.Println("foobar")
            } else {
                    fmt.Println("None matched")
            }
            fmt.Println("thank you!")

    }
    ```

    * None matched<br/>thank you!
    * bar<br/>thank you!
    * foobar<br/>thank you!
    * foo<br/>thank you!

    <details>
    <summary>Reveal</summary>

    > bar<br/>thank you!

    This one has a gotcha! Note this bit

    ```go
        } else if a+b == "foobar" {
                fmt.Println("bar")
        } else if a+b == "foobar" {
                fmt.Println("foobar")
        } ...
    ```

    `a+b` is indeeed `foobar` and it matches both of the above. Go will choose the first match and ignore any others that match, therefore the output is `bar` and not `foobar`

    </details>
    </details>

1.  <details>
    <summary>Can we use if block independently, without else-if and else blocks?</summary>

    1. No, we need at least one else block.
    1. else-if is optional, but if block would raise error without else block.
    1. Yes, we can write if block without any of the other blocks.
    1. We need at least one if, one else-if and one else block for program to compile successfully.


    * false<br/>true

    <details>
    <summary>Reveal</summary>

    > C

    Just like speech. You don't always need to say "else" or "else if" after if.

    </details>
    </details>

