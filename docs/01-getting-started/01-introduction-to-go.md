# Lab: Introduction to Go

[Take me to the lab!](https://kodekloud.com/topic/lab-introduction-to-go/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).

1.  <details>
    <summary>Where was the Go programming language designed ?</summary>

    * VMware
    * Facebook
    * Google
    * Microsoft

    <details>
    <summary>Reveal</summary>

    > Google

    </details>
    </details>

1.  <details>
    <summary>Go was created to support the following</summary>

    1. The ease of programming of an interpreted, dynamically typed language.
    1. For creating web pages easily.
    1. Provide the efficiency and safety of a statically typed, compiled language.
    1. Aimed to be modern, with support for networked and multicore computing.

    <details>
    <summary>Reveal</summary>

    > A, C, D

    Although Go is *not* dynamically typed or interpreted, the language was created with simplicity in mind to make it feel like using a language like Python which is these things.

    It's not for creating web *pages*. That's HTML and JavaScript.

    Compiled languages with static types provide safety - many bugs are caught by the compiler before you even get to run the program. Static typing provides efficiency because dynamic typing requires much more work behind the scenes (runs slower as a result).

    Go has support built into the language itself for multicore computing such as "channels". You will learn about these in the Advanced Golang course. It also has great package support for networking - it's simple to construct API servers.

    </details>

    </details>

1.  <details>
    <summary>Go is a...</summary>

    * compiled language
    * interpreted language

    <details>
    <summary>Reveal</summary>

    > compiled language

    </details>
    </details>

1.  <details>
    <summary>What is a package in go?</summary>

    1. a file that ends with `.mod` extension.
    1. a file that ends with `.go` extension
    1. a collection of files that live in the same directory and have the same package statement at the beginning.
    1. Set of core packages to enhance and extend the language.

    <details>
    <summary>Reveal</summary>

    > C

    </details>
    </details>

1.  <details>
    <summary>In a Go program, where are packages declared ?</summary>

    * At the start of the program
    * After the import staetment
    * At the end of the program
    * Anywhere in the code.

    <details>
    <summary>Reveal</summary>

    > At the start of the program

    The first line of every `.go` file that is not a blank line or a comment must be a `package` statement to declare the package that the code belongs to.

    </details>
    </details>

1.  <details>
    <summary>Choose the correct format of importing a package in Go:</summary>

    If we wanted to import the `fmt` package, which is the correct syntax?

    * `import fmt`
    * `import (fmt)`
    * `import "fmt"`
    * `"import fmt"`

    <details>
    <summary>Reveal</summary>

    > `import "fmt"`

    `import` is a keyword so must not be enclosed within quotes. The name of the package must be quoted.

    </details>
    </details>

1.  <details>
    <summary>What is the entry point in a Go program?</summary>

    * The function that's declared last
    * The `main` function
    * Function imported by `fmt` package
    * The function that's declared first

    <details>
    <summary>Reveal</summary>

    > The `main` function

    The go runtime looks for a function called `main` and calls it. That's how the program starts. This is taken from the venerable C language!

    </details>

    </details>

1.  <details>
    <summary>Which package consists of <b>main()</b> function ?</summary>

    * independent of package name
    * package `main`
    * we can create our own main function, no package needs to be imported
    * package `greetings`

    <details>
    <summary>Reveal</summary>

    > package `main`

    By convention, you create the `main` package first, and put the `main()` function in it:

    ```go
    package main

    // Imports go here - if you need any

    func main() {
        // your program starts here
    }
    ```

    </details>
    </details>

1.  <details>
    <summary>Our program began with package main, what would the files in the fmt package begin with?</summary>

    * `package os`
    * `package fmt`
    * `pacakge object`
    * `package main`

    <details>
    <summary>Reveal</summary>

    > `package fmt`

    `fmt` is a package, which is meant to be imported by other programs. Here's a snippet of one of the files from this package:

    ```go
    package fmt

    import (
        "internal/fmtsort"
        "io"
        "os"
        "reflect"
        "strconv"
        "sync"
        "unicode/utf8"
    )

    // Some lines removed for brevity

    // Printf formats according to a format specifier and writes to standard output.
    // It returns the number of bytes written and any write error encountered.
    func Printf(format string, a ...any) (n int, err error) {
        return Fprintf(os.Stdout, format, a...)
    }

    ```

    </details>
    </details>

1.  <details>
    <summary>Choose the correct syntax to write a comment in Go</summary>

    1.  ```python
        # this is a comment
        ```

    1.  ```go
        // this is a comment
        ```

    1.  ```go
        /*
        this is
        a multiline
        comment
        */
        ```

    1.  ```python
        """
        this is
        a multiline
        comment
        """

    <details>
    <summary>Reveal</summary>

    > B, C

    The other two commenting styles are those of Python.

    </details>
    </details>

1.  <details>
    <summary>Now let's run some go commands using the terminal. Open an new terminal and identify the version of go installed.</summary>

    In the VSCode terminal window, run the following:

    ```
    go version
    ```

    Select the appropriate answer.

1.  <details>
    <summary>Which of the following commands is not valid?</summary>

    If unsure, run `go help` and check out the commands and their uses.

    * go version
    * go run
    * go compile
    * go generate

    <details>
    <summary>Reveal</summary>

    > go compile

    This is not valid, because the command to compile without running is `go build`.

    </details>
    </details>

1.  <details>
    <summary>A simple go program has been created for you at the location /root/code/simple-project. However, there is an error in the code.</summary>

    Identify and fix the problem.

    1. In the explorer pane, click on `simple-project` to reveal `main.go`
    1. Click on `main.go` to load it into the editor.

    Review the answer to question 6 to know the issue, then edit the code so it is correct.

    <details>
    <summary>Reveal</summary>

    > Packages imported with the `import` statement must have the package name in double-quotes.

    Fix the import statement thus:

    ```go
    import "fmt"
    ```

    </details>
    </details>



