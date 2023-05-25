# Lab: Function Syntax

[Take me to the lab!](https://kodekloud.com/topic/lab-return-types-multiple-named-variadic/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    func doSomething(int, int) int {
            return "2"
    }

    func main() {
            fmt.Println(doSomething(1, 2))
    }
    ```

    * 1 2<br/>1
    * error
    * "2"
    * 2

    <details>
    <summary>Reveal</summary>

    > error

    The program would not complile. The function return type is `int` therefore it cannot return the string `"2"`

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    func calcSquare(numbers []int) []int {
            squares := []int{}
            for _, v := range numbers {
                    squares = append(squares, v*v)
            }
            return squares

    }

    func main() {
            nums := [3]int{10, 20, 15}
            fmt.Println(calcSquare(nums[:]))
    }
    ```

    * [10 20 15]
    * [100 400 900]
    * Error
    * [100 400 225]

    <details>
    <summary>Reveal</summary>

    > [100 400 225]

    * The function accepts an `int` slice and returns an `int` slice
    * `nums[:]` is the correct way to pass the array `nums` to the function as a slice
    * The `for` loop in the function builds a slice of the squares of the values in the input slice
    * The return value of the function is printed

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    func calcSquare(numbers []int) ([]int, bool) {
            squares := []int{}
            for _, v := range numbers {
                    squares = append(squares, v*v)
            }
            return squares, true

    }

    func main() {
            nums := [3]int{10, 20, 15}
            fmt.Println(calcSquare(nums[:]))
    }
    ```

    * [100 400 225] true
    * [100 400 225]
    * [10 20 15]
    * Error


    <details>
    <summary>Reveal</summary>

    > [100 400 225] true

    This is almost the same as the previous question. The difference is that the function has two return values: `[]int` and `bool`

    `squares` and `true` are returned by the function, and are printed.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    func printStrings(s string, names ...string) {
            fmt.Println(s)
            for _, value := range names {
                    fmt.Printf("%s, ", value)
            }

    }

    func main() {
            printStrings("Hey there", "Joe", "Monica", "Gunther")
    }
    ```

    * Hey there<br/>Joe, Monica, Gunther
    * Hey there, Joe, Monica, Gunther,
    * Hey there<br/>Joe,<br/>Monica,<br/>Gunther,
    * Hey there<br/>Joe, Monica, Gunther,

    <details>
    <summary>Reveal</summary>

    > Hey there<br/>Joe, Monica, Gunther,

    * The function `printStrings` has two argumentsL: `s` and `names`
    * `s` will get the first string passed to the function call (i.e. `Hey there`)
    * `names` is variadic so will be represented as a slice of strings, and gets everything that follows `Hey there`
    * The value of `s` is printed on its own line
    * The remaining values are printed on the same line with a comma following each.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    func printStrings(names ...string) (names_c []string) {
        names_c := []string {}
            for _, value := range names {
                    names_c = append(names_c, strings.ToUpper(value))
            }
            return
    }

    func main() {
            result := printStrings("Joe", "Monica", "Gunther")
            fmt.Println(result)
    }
    ```

    * No output
    * [JOE MONICA GUNTHER]
    * Error
    * Joe, Monica, Gunther,

    <details>
    <summary>Reveal</summary>

    > Error

    This is a tricky one to spot!

    Firstly note that to be able to try to run this program we need an additional import! `import "strings"` is required for `strings.ToUpper`

    Now you've put `package main` and imported `"strings"` and `"fmt"`, there is still a compilation error, which is why the answer is "Error".

    The message `no new variables on left side of :=` means that you are trying to create a new variable using the name of a vairable that already exists. It's complaining about `names_c`. Why? Because the function uses a *named* return type: `(names_c string)`. This means that the variable `names_c` is already declared within the scope of the function, and why it ends with `return` and not `return names_c`.

    To fix the compilation error we would change the line<br/>`names_c := []string {}`<br/>to<br/>`names_c = []string {}` - try it!

    </details>
    </details>

