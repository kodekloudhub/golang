# Lab: Pointers

[Take me to the lab!](https://kodekloud.com/topic/lab-pointers/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).

1.  <details>
    <summary>What would be the output of the following program:</summary>

    Note: add package and import statements as needed

    ```go
    package main

    import (
        "fmt"
    )

    func modify(y int) int {
        y += 15
        return y
    }
    func main() {
        y := 20
        modify(y)
        fmt.Println(y)
    }
    ```

    * 35
    * 20
    * error
    * 15

    <details>
    <summary>Reveal</summary>

    > 20

    Contrary to how the function is named, the value of `y` in `main` is *not* modified. A *copy* of `y` is modified inside the `modify` function and the modified value returned, however the return value isn't used.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    Note: add package and import statements as needed

    ```go
    func main() {
        y := [3]int{10, 20, 30}
        py := &y
        fmt.Printf("%T %v \n", py, *py)
    }
    ```

    * *[]int<br/>[10 20 30]
    * *int [10 20 30]
    * *[3]int
    * *[3]int [10 20 30]

    <details>
    <summary>Reveal</summary>

    > *[3]int [10 20 30]

    * The assignment `py` is creating a pointer variable, as it takes the address of `y` using the `&` operator.
    * The type of `py` is therefore `*[3]int` because it *points to* a `[3]int`, so that's what gets printed by the `%T` formatter.
    * Lastly, we get the array content printed with the `%v` formatter, because `py` has been dereferenced with the `*` operator, turning it back into a real `[3]int`

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    Note: add package and import statements as needed

    ```go
    func main() {
        y := [3]int{10, 20, 30}
        fmt.Printf("%v \n", y)
        (*&y)[0] = 100
        fmt.Printf("%v \n", y)
    }
    ```

    * [10 20 30]<br/>[100]
    * [10 20 30]<br/>[100 20 30]
    * Error
    * [10 20 30]<br/>[10 20 30]

    <details>
    <summary>Reveal</summary>

    > [10 20 30]<br/>[100 20 30]

    * The first `Printf` prints the array `y` and a newline.
    * `(*&y)` first creates a pointer to `y` with `&`, then immediately dereferences it with `*`, effectively giving us `y` again, so the whole statement `(*&y)[0] = 100` has exactly the same effect as `y[0] = 100`.
    * Print the array again, and the first element as expected is `100`

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    Note: add package and import statements as needed

    ```go
    func main() {
        var y int
        var ptr *int = &y

        *ptr = 0
        fmt.Println(y)

        *ptr += 5
        fmt.Println(y)
    }
    ```

    * 5<br/>0
    * 0<br/>5
    * 0<br/>0
    * error

    <details>
    <summary>Reveal</summary>

    > 0<br/>5

    * Create a pointer to `y` as variable `ptr`
    * Set the actual value of `y` to zero via a pointer deference, then print `y`
    * Set the actual value of `y` to 5 via a pointer deference, then print `y`

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    Note: add package and import statements as needed

    ```go
    func main() {
        var y int
        var ptr *int = &y
        fmt.Println(y)
        fmt.Println(*ptr)
    }
    ```

    1. 0<br/>&lt;nil&gt;
    1. 0<br/>0
    1. &lt;nil&gt;<br/>&lt;nil&gt;
    1. &lt;nil&gt;<br/>0

    <details>
    <summary>Reveal</summary>

    > B

    * Declare variable y as `int`. Because it has no assignment, it will have the default value zero.
    * Create a pointer to `y` as variable `ptr`. This pointer cannot be `<nil>` because it has the address of an existing variable which is never `<nil>`
    * Print `y`, which we know is zero.
    * Print the dereferenced value of the pointer, which is the value of `y`, i.e. zero.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    Note: add package and import statements as needed

    ```go
    func main() {
        s := 100
        var ptr *string = &s
        fmt.Println(s)
        *ptr += 100
        fmt.Println(s)
    }
    ```

    * 100
    * 200
    * 100<br/>200
    * error

    <details>
    <summary>Reveal</summary>

    > error

    * The variable `s` is initialized as an `int` by assigning `100` to it.
    * The next line is declaring a pointer to `string`, which cannot assume the address of an integer variable. Note that in languages like C, this kind of assignment *would* be allowed and would make for hard to find bugs unless you knew exactly what you were doing!

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    Note: add package and import statements as needed

    ```go
    func main() {
        s := "hello"
        var ptr *string = &s
        fmt.Println(s)
        *ptr += strings.ToUpper(s)
        fmt.Println(s)
    }
    ```

    * hello<br/>hello HELLO
    * hello<br/>helloHELLO
    * HELLO<br/>hello
    * hello<br/>hello

    <details>
    <summary>Reveal</summary>

    > hello<br/>helloHELLO

    1. Declare `s` as a string with value `hello`
    1. Create a pointer to `s` as `ptr`.
    1. Print the value of `s` with a newline.
    1. Via the pointer, append uppercase version of `s` to `s`<br/>`*ptr += strings.ToUpper(s)` is equivalent to `s += strings.ToUpper(s)`
    1. Print the new value of `s`

    </details>
    </details>

