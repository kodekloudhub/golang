# Lab: Assignment Operators

[Take me to the lab!](https://kodekloud.com/topic/lab-logical-operators/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).

See also [Assignment](https://go.dev/ref/spec#Assignment_statements) in the Go manual.

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
            var x, y string = "foo", "bar"
            x += y
            fmt.Println(x)
    }
    ```

    * foobar
    * foo
    * error
    * bar

    <details>
    <summary>Reveal</summary>

    > foobar

    `+=` is "add and assign", and is equivalent to `x = x + y`. When you add two strings, the result is the concatenation of the strings.

    </details>
    </details>

1.  <details>
    <summary>What would be the output for the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            var x, y int = 27, 7
            x /= y
            fmt.Println(x)
    }
    ```

    * 6
    * 3
    * error
    * 6.00

    <details>
    <summary>Reveal</summary>

    > 3

    `/=` is "divide and assign", and is equivalent to `x = x / y`. Since we have two integers, then an integer division is performed and the remainder is discarded: `27 / 7 = 3 r6`

    </details>
    </details>

1.  <details>
    <summary>What would be the output for the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            var x, y float64 = 27.9, 7.0
            x -= y
            fmt.Println(x)
            x += y
            fmt.Println(x)
    }
    ```

    * 27.9<br/>20.9
    * 20.9<br/>27.9
    * 20.9<br/>7.9
    * 27.9<br/>9.0

    <details>
    <summary>Reveal</summary>

    > 20.9<br/>27.9

    * `x -= y` ... x = 27.9 - 7.0 = 20.9, then
    * `x += y` ... x = 20.9 + 7.0 = 27.9

    </details>
    </details>

1.  <details>
    <summary>What would be the output for the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            var x, y int = 100,9
            x /= y
            fmt.Println(x)
            x %= y
            fmt.Println(x)
    }
    ```

    * 2<br/>2
    * 11<br/>2
    * 2<br/>11
    * 11<br/>11

    <details>
    <summary>Reveal</summary>

    > 11<br/>2

    * `x /= y` ... x = 100 / 9 = 11. Remember this is an integer division so the remainder is discarded, then
    * `x %= y` ... x = 11 % 9 = 2. `x` is now 11 from the previous division assignment. Remainder of 11 divided by 2 is 2.

    </details>
    </details>

1.  <details>
    <summary>Which of these operator assigns the remainder of the division x</summary>

    * `/=`
    * `*=`
    * `%=`
    * `\=`

    <details>
    <summary>Reveal</summary>

    > `%=`

    This is the modulo (remainder) assignment operator.

    * `/=` is divide assign
    * `*=` is multiply assign
    * `\=` is a syntax error and won't compile.

    </details>
    </details>

