# Lab: Bitwise Operators

[Take me to the lab!](https://kodekloud.com/topic/lab-arithmetic-operators/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).

See also [Arithmetic Operators](https://go.dev/ref/spec#Arithmetic_operators) in the Go manual. Bitwise operators are considered arithmetic.

Refer to the following logic truth table to help with understanding the answers

| a     | b     | a AND b | a OR b | a XOR b |NOT a | NOT b |
|-------|-------|---------|--------|---------|------|-------|
| false | false | false   | false  | false   |true  | true  |
| true  | false | false   | true   | true    |false | true  |
| false | true  | false   | true   | true    |true  | false |
| true  | true  | true    | true   | false   |false | false |


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
    <summary>Select the correct statements:</summary>

    1. bitwise AND takes two numbers and does OR on every bit of two numbers.
    1. bitwise OR takes two numbers and does OR on every bit of two numbers.
    1. bitwise AND takes two numbers and does AND on every bit of two numbers.
    1. bitwise OR takes two numbers and does AND on every bit of two numbers.

    <details>
    <summary>Reveal</summary>

    > B, C

    A and D are nonsense!

    </details>
    </details>

1.  <details>
    <summary>Find the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            var x, y int = 100,90
            fmt.Println(x & y)
            fmt.Println(x | y)
    }
    ```

    * 90<br/>100
    * 64<br/>126
    * 0<br/>109
    * 64<br/>96

    <details>
    <summary>Reveal</summary>

    > 64<br/>126

    To understand how this works, we must first convert both numbers to binary, then apply logic truth table to each column of digits. In binary, `true` is `1` and `false` is 0. Convert the binary result back to decimal.

    ```
      01100100  (100)
    & 01011010  ( 90)
      --------
      01000000  ( 64)

      01100100  (100)
    | 01011010  ( 90)
      --------
      01111110  (126)
    ```

    </details>
    </details>

1.  <details>
    <summary>Select the correct statements</summary>

    1. The result of XOR is 0 when the two bits are same.
    1. The result of XOR is 1 when the two bits are opposite.
    1. The result of XOR is 0 when the two bits are opposite.
    1. The result of XOR is 1 when the two bits are same.


    <details>
    <summary>Reveal</summary>

    > A, B

    Refer to above truth table.

    </details>
    </details>

1.  <details>
    <summary>Find the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            var x, y int = 100,90
            fmt.Println((x+y) >> 2)
    }
    ```

    * 47
    * 90
    * 83
    * 56

    <details>
    <summary>Reveal</summary>

    > 47

    `>>` is the bitwise shift right operator. The number of places to shift by in this case is 2. To understand how this works requires a few steps

    1. Do the addition `x+y` and get the result. 100 + 90 = 190
    2. Convert this result to binary: `10111110`
    3. Now shift right by two columns. Anything that "falls off the end" is discarded. Zeros come in from the left.

        ```
        Shift 1: `01011111`
        Shift 2: `00101111`
        ```
    4. Convert this binary result back to decimal: `00101111` = `47`

    </details>
    </details>

1.  <details>
    <summary>Find the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            var x, y int = 100,90
            fmt.Println(!(((x+y) >> 2 ) == 47))
    }
    ```

    * 47
    * error
    * true
    * false

    <details>
    <summary>Reveal</summary>

    > false

    There's a lot going on here! To understand how this works requires a few steps. The order we evaluate this expression is determined by the bracketing. We can also tell that the result must be boolean `true` or `false`, as the final evaluation will be a logical NOT of a boolean comparision using `==` so that rules out `47` as being a correct answer. There are no syntax errors or anything that would cause a runtime error (like division by zero), so `error` is also not the correct answer.

    We have to start on the inside and work out.

    1. The first part is `((x+y) >> 2)` which we did in the previous question, and the result is `47`.
    2. The next part is `(((x+y) >> 2 ) == 47)`, i.e. `47 == 47` which is `true`
    4. Finally `!(((x+y) >> 2 ) == 47)`, i.e. `NOT (47 == 47)`, which is `false` and is therefore the answer to this question.

    </details>
    </details>

