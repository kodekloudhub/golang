# Lab: Looping with For

[Take me to the lab!](https://kodekloud.com/topic/lab-switch-statement/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).

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
    <summary>What would be the output of the following program -</summary>

    ```go
    package main

    import "fmt"

    func main() {
            for {
                    fmt.Println("Hello World!")
            }
    }
    ```

    * Infinite loop
    * Syntax error
    * Hello World!
    * No output

    <details>
    <summary>Reveal</summary>

    > Infinite loop

    * Yes, it will print "Hello World!", but it will print it an infinite number of times, or until you forcibly stop to program with `CTRL-C`.
    * It is infinite because the `for` has no condition with which to exit.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program -</summary>

    ```go
    package main

    import "fmt"

    func main() {
            i := 3
            for i > 10 {
                    fmt.Println(i * 2)
                    i += 1
            }
    }
    ```

    * No output
    * Syntax error
    * 3<br/>4<br/>5<br/>6<br/>7<br/>8<br/>9
    * 6<br/>8<br/>10<br/>12<br/>14<br/>16<br/>18

    <details>
    <summary>Reveal</summary>

    > No output

    The loop condition is "i is greater than 10". `i` is 3 when the program reaches `for`, thus the conditon is false and the body of the loop is not executed.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program -</summary>

    ```go
    package main

    import "fmt"

    func main() {
            i := 5
            j := 0
            for j < 5 {
                    fmt.Println(i * 2)
                    j += 1
            }
    }
    ```

    * Syntax error
    * Infinite loop
    * 10<br/>10<br/>10<br/>10<br/>10
    * 0<br/>2<br/>4<br/>6<br/>8

    <details>
    <summary>Reveal</summary>

    > 10<br/>10<br/>10<br/>10<br/>10

    * At the entry to the loop, `j` is initially zero. This satisfies the loop condition so the loop content is executed.
    * `i` is `5`, and remains `5` for the duration of the program. This means the `Println` will *always* print `10`.
    * Each time round the loop, `j` is incremented, therefore after the fifth execution of the loop, `j` will now be `5` and the loop condition will be `false`, so the loop exits.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program -</summary>

    ```go
    package main

    import "fmt"

    func main() {
        for i := 0; i <= 5; i++ {
            fmt.Println(i * i)
            if i == 3 {
                continue
            }
        }
    }
    ```

    * 0<br/>1<br/>4
    * Error
    * 0<br/>1<br/>4<br/>16<br/>25
    * 0<br/>1<br/>4<br/>9<br/>16<br/>25


    <details>
    <summary>Reveal</summary>

    > 0<br/>1<br/>4<br/>9<br/>16<br/>25

    This is a program to print squares of numbers from zero to 5 inclusive - and that's what it does - it prints all of them!

    This is a red herring

    ```go
        if i == 3 {
             continue
        }
    ```

    The `continue` statement directs the program to go directly back to the `for` without executing any further code within the `for`'s block. However there is nothing following the `continue` so the net effect is not to change the flow of the program, i.e nothing is missed out.

    </details>
    </details>


1.  <details>
    <summary>What would be the output of the following program -</summary>

    ```go
    package main

    import "fmt"

    func main() {
        for i := 0; i <= 5; i++ {
            if i == 3 {
                break
            }
            fmt.Println(i * i)
        }
    }
    ```

    * 0<br/>1<br/>4
    * Error
    * 0<br/>1<br/>4<br/>9
    * 0<br/>1<br/>4<br/>9<br/>16<br/>25


    <details>
    <summary>Reveal</summary>

    > 0<br/>1<br/>4<br/>9

    This is very similar to the previous question - it's still a program to print squares, however the for loop finishes early due to the `break` statement when `i` is 3.

    It has already printed the square of 3, thus the output gets as far as 9. But then `i == 3` is `true` and the `break` within the `if` block is executed. `break` moves control to whatever follows the `}` of the for loop - in this case the end of the program.

    </details>
    </details>
