# Lab: Logical Operators

[Take me to the lab!](https://kodekloud.com/topic/lab-logical-operators/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).

See also [Logical Operators](https://go.dev/ref/spec#Logical_operators) in the Go manual.

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
            var a, b bool = true, false
            fmt.Println(a && b)
            fmt.Println(a || b)
    }
    ```

    * false<br/>true
    * false<br/>false
    * true<br/>true
    * true<br/>false

    <details>
    <summary>Reveal</summary>

    > false<br/>true

    `&&` is the AND operator. `||` is the OR operator. As will be seen later, `!` is the NOT operator.

    Refer logic truth table

    | a     | b     | a AND b | a OR b | a XOR b |NOT a | NOT b |
    |-------|-------|---------|--------|---------|------|-------|
    | false | false | false   | false  | false   |true  | true  |
    | true  | false | false   | true   | true    |false | true  |
    | false | true  | false   | true   | true    |true  | false |
    | true  | true  | true    | true   | false   |false | false |

    It should be noted that Go does not provide a logical XOR (exclusive-OR) operator where many other languages do, however XOR for two `bool` variables can be expressed like this: `(a != b)`.
    </details>
    </details>

1.  <details>
    <summary>What would be the output for the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            var a, b bool = false, false
            fmt.Println(a && b)
            fmt.Println(a || b)
    }
    ```

    * false<br/>true
    * false<br/>false
    * true<br/>true
    * true<br/>false

    <details>
    <summary>Reveal</summary>

    > false<br/>false

    Refer boolean truth table in the answer to Q1 above

    </details>
    </details>

1.  <details>
    <summary>What would be the output for the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            var a, b bool = false, true
            fmt.Println(!a)
            fmt.Println(b)
    }
    ```

    * false<br/>true
    * false<br/>false
    * true<br/>true
    * true<br/>false

    <details>
    <summary>Reveal</summary>

    > true<br/>true

    Refer boolean truth table in the answer to Q1 above

    In the first `Println` we have applied the logical NOT (`!`) operator to the value of `a`. NOT false = true.

    </details>
    </details>

1.  <details>
    <summary>What would be the output for the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            var a bool = false
            result := 10 > 50
            fmt.Println(!(a && result))
    }
    ```

    * false
    * error
    * 1
    * true

    <details>
    <summary>Reveal</summary>

    > true

    Refer boolean truth table in the answer to Q1 above

    Let's break it down:

    * `result := 10 > 50`. This creates `result` as a `bool` variable, holding the value of `10 > 50` which is `false`.
    * Next, the bracketed expression is evaluated `(a && result)`. `a` is `false`, `result` is `false` therefore this evaluates to `false`.
    * Finally, NOT is applied to the result of the previous evaluation, therefore answer is `true`.

    </details>
    </details>

1.  <details>
    <summary>What would be the output for the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            var a bool = true
            result := 10 > 50
            fmt.Println(!(a || result))
    }
    ```

    * false
    * error
    * 1
    * true

    <details>
    <summary>Reveal</summary>

    > true

    Refer boolean truth table in the answer to Q1 above

    Let's break it down:

    * `result := 10 > 50`. This creates `result` as a `bool` variable, holding the value of `10 > 50` which is `false`.
    * Next, the bracketed expression is evaluated `(a || result)`. `a` is `true`, `result` is `false` therefore this evaluates to `true`.
    * Finally, NOT is applied to the result of the previous evaluation, therefore answer is `false`.

    </details>
    </details>

