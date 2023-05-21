# Lab: Comparison Operators

[Take me to the lab!](https://kodekloud.com/topic/lab-comparison-operators/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).

See also [Comparison Operators](https://go.dev/ref/spec#Comparison_operators) in the Go manual.

1.  <details>
    <summary>What would be the output of the following comparison -</summary>

    ```go
    var a, b string = "Cat", "cat"
    fmt.Println(a == b)
    ```

    * Error
    * False
    * True
    * 0

    <details>
    <summary>Reveal</summary>

    > False

    "Cat" does not equal "cat". Difference in capitalisation.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following comparison -</summary>

    ```go
    var a string = "cat"
    var b int = 12
    fmt.Println(a == b)
    ```

    * Error
    * 1
    * False
    * True

    <details>
    <summary>Reveal</summary>

    > Error

    The program would not compile due to strict type checking performed by the compiler. You cannot compare `int` with `string`.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following comparison -</summary>

    ```go
    var a int = 12
    var b int = 12
    fmt.Println(a != b)
    ```

    * True
    * 1
    * Error
    * False

    <details>
    <summary>Reveal</summary>

    > False

    The values of `a` and `b` are equal, therefore `!=` will be false.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following comparisons -</summary>

    ```go
    func main() {
            var a int = 12
            var b int = 12
            fmt.Println(a <= b)

            a = 20
            fmt.Println(a <= b)

            b = 100
            fmt.Println(a <= b)

            c := 0
            fmt.Println(a <= c)
    }
    ```

    * false<br/>false<br/>true<br/>true
    * true<br/>true<br/>false<br/>false
    * true<br/>false<br/>true<br/>false
    * true<br/>true<br/>true<br/>true

    <details>
    <summary>Reveal</summary>

    > true<br/>false<br/>true<br/>false

    Let's break it down:

    * At the first comparison, `a` = 12 and `b` = 12. 12 less than or equal to 12 is `true` (because they're equal).
    * At the second comparison, `a` is now 20 and `b` is still 12. 20 less than or equal to 12 is `false`.
    * At the third comparison, `a` is still 20 and `b` is now 100. 20 less than or equal to 100 is `true`.
    * At the final comparison, `a` is still 20 and new variable `c` is zero. 20 less than or equal to 0 is `false`.

    </details>
    </details>

1.  <details>
    <summary>Which operator can you use to validate if two values are not equal</summary>

    * `<=`
    * `!=`
    * `>=`
    * `<`

    <details>
    <summary>Reveal</summary>

    > `!=`

    As for the others:

    * `<=` - Less than or equal to
    * `>=` - Greater than or equal to
    * `<` - Less than

    </details>
    </details>

