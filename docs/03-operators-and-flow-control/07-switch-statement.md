# Lab: Switch Statement

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

Note that switch statements are nothing more than a shorthand way of writing if - else if - else if - else, where `default` is the final `else`

### Questions

1.  <details>
    <summary>What would be the output of the following program -</summary>

    ```go
    package main

    import "fmt"

    func main() {
            var a, b = 100, 5
            switch {
            case a/b == 10:
                    fmt.Println("10")
            case a/b == 20:
                    fmt.Println("20")
            case a/b == 10:
                    fmt.Println("30")
            default:
                    fmt.Println("default")
            }

    }
    ```

    * 30
    * 40
    * 10
    * 20

    <details>
    <summary>Reveal</summary>

    > 20

    1. Work out `a/b`. `100/5 = 20`
    2. Examine the case statements for the one that matches the above evaluation.


    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program -</summary>

    ```go
    package main

    import "fmt"

    func main() {
            day := "sunday"
            switch day {
            case "monday":
                    fmt.Println("monday")
            case "tuesday":
                    fmt.Println("tuesday")
            case "wednesday":
                    fmt.Println("wednesday")
            case "thursday":
                    fmt.Println("thursday")
            case "friday":
                    fmt.Println("friday")
            case "saturday", "sunday":
                    fmt.Println("weekend")
            default:
                    fmt.Println("default")
            }
    }
    ```

    * friday<br/>sunday
    * weekend<br/>default
    * weekend
    * saturday<br/>weekend

    <details>
    <summary>Reveal</summary>

    > weekend

    * It will switch on the value of `day` which is `sunday`
    * It will match on the final case, which is checking for `saturday` *or* `sunday`
    * No `default` case will be selected, as we already have a match.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program -</summary>

    ```go
    package main

    import "fmt"

    func main() {
            day := "wednesday"
            switch day {
            case "monday":
                    fmt.Println("monday")
            case "tuesday":
                    fmt.Println("tuesday")
            case "wednesday":
                    fmt.Println("wednesday")
                    fallthrough
            case "thursday":
                    fmt.Println("thursday")
                    fallthrough
            case "friday":
                    fmt.Println("friday")
            case "saturday", "sunday":
                    fmt.Println("weekend")
            default:
                    fmt.Println("default")
            }
    }
    ```

    * wednesday<br/>thursday
    * wednesday<br/>thursday<br/>friday<br/>default
    * wednesday<br/>thursday<br/>friday
    * wednesday<br/>friday<br/>default

    <details>
    <summary>Reveal</summary>

    > wednesday<br/>thursday<br/>friday

    * It will switch on the value of `day` which is `wednesday`
    * It will match `case "wednesday"`
    * It then encounters `fallthrough`, which means run the code in the `case` that follows *irrespective* of whether the case condition matches, thus `thursday` is printed. Similar for `friday`, but there's no `fallthrough` in friday's case, so `default` is not printed.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program -</summary>

    ```go
    package main

    import "fmt"

    func main() {
            var a, b = 100, 5
            switch a {
            case a/b == 10:
                    fmt.Println("10")
            case a/b == 20:
                    fmt.Println("20")
            case a/b == 10:
                    fmt.Println("30")
            default:
                    fmt.Println("default")
            }
    }
    ```

    * 30
    * Error
    * 10
    * 20

    <details>
    <summary>Reveal</summary>

    > Error

    At first glance this looks like Q1, but there is a subtle difference! This time it's not an unbounded switch, it is switching on the value of `a`, and `a` is an `int`.

    The comparisons for the cases are all boolean which can't be tested against the integer switch variable `a`, so you will get a compilation error.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program -</summary>

    Note: When using switch with conditionals - we don't specify expression after switch. This is what the error was in the last question.

    ```go
    package main

    import "fmt"

    func main() {
            var i, j = 10, 50

            switch {
            case i+j == 60:
                    fmt.Println("equal to 60")
            case i+j <= 60:
                    fmt.Println("less than or equal to 60")
                    fallthrough
            default:
                    fmt.Println("greater than 60")
            }
    }
    ```

    * less than or equal to 60<br/>greater than 60
    * equal to 60
    * less than or equal to 60<br/>equal to 60
    * less than or equal to 60<br/>greater than 60

    <details>
    <summary>Reveal</summary>

    > equal to 60

    1. Evaluate `i+j` - 10+50 = 60
    1. The first case matches, so `equal to 60` is printed.
    1. There is no `fallthrough` on this case, so the switch is complete and no other case is considered.

    </details>
    </details>

