# Lab: Data types and Variables

[Take me to the lab!](https://kodekloud.com/topic/lab-data-types-and-variables/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).

1.  <details>
    <summary>Which of the following methods is used to take input from user?</summary>

    1. `fmt.Scanf`
    1. `fmt.Printf`
    1. `fmt.Scan`
    1. `fmt.Println`

    <details>
    <summary>Reveal</summary>

    > `fmt.Scanf`

    Any `Print` function outputs to the console, rather than inputs anything.

    Actually both `Scan` and `Scanf` can read user input, but the latter is more versatile.

    </details>
    </details>

1.  <details>
    <summary>What does the Scanf function return?</summary>

    1. It returns the number of arguments that the function writes to
    1. It returns a boolean variable denoting if the function was successful or not
    1. It returns the error thrown during the execution of the program
    1. It does not return anything.

    <details>
    <summary>Reveal</summary>

    > A, C

    `Scanf` is an example of a function that returns more than one value. Many functions in Go return a value and an error. If the error is `nil` then the other return value is the actual value you want and is valid.

    The wording of answer 3 is a little misleading. It is actually the error rasied during execution of `Scanf` itself, if an error occurred. A likely error is if you expected to scan a number and text was entered.

    </details>
    </details>

1.  <details>
    <summary>From the following code snippets - select the correct one that takes in multiple inputs and is syntactically correct</summary>

    1.  ```go
        var name string
        var b bool

        fmt.Scanf("%s", &name)
        fmt.Scanf("%t", &b)
        ```


    1.  ```go
        var name string
        var b bool

        fmt.Scanf("%t", name)
        fmt.Scanf("t", b)
        ```

    1.  ```go
        var name string
        var b bool

        fmt.Scanf("%s %t", &name, &b)
        ```

    1.  ```go
        var name string
        var b bool

        fmt.Scanf("%d %t", name, b)
        ```

    <details>
    <summary>Reveal</summary>

    > A, C

    The format specifier for string is `%s` and for bool is `%t`. Thus B and D are incorrect due to incorrect (`%d`) or invalid (`t`) format specifiers.

    We must always pass the address of a variable we want `Scanf` to write to, i.e use `&` prefix. This also rules out B and D.

    A is correct because it scans a string (`%s`) to a string var (`&name`), then in the second statement does the same with a boolean var.

    C is correct as it scans a string and a boolean separated by a space into corresponding string and boolean variables.

    </details>
    </details>

1.  <details>
    <summary>Select the correct code snippet for determining type of variable</summary>

    1.  ```go
        var grades int = 42
        fmt.Printf("variable grades = %v is of type %v \n", grades, grades)
        ```

    1.  ```go
        var grades int = 42
        fmt.Printf("variable grades = %v is of type %t \n", grades, grades)
        ```

    1.  ```go
        var grades int = 42
        fmt.Printf("variable grades = %v is of type %T \n", grades, grades)
        ```

    1.  ```go
        var grades int = 42
        fmt.Printf("variable grades = %v is of type %v \n", grades, type(grades))
        ```

     <details>
    <summary>Reveal</summary>

    > C

    Know that `%T` is the correct format specifier for printing the type of a varaible.

    `type()` is not a valid built-in function.

    `%v` prints the "default" format of the variable associated with it, so for an integer it's the same as `%d`.

    </details>
    </details>

1.  <details>
    <summary>The function <b>TypeOf()</b?> - used for determining data type of a variable belongs to which package</summary>

    <details>
    <summary>Reveal</summary>

    > `reflect`

    Determining runtime type of a variable is a reflection operation.

    </details>
    </details>

1.  <details>
    <summary>We can use <b>reflect.TypeOf()</b> to determine type of a</summary>

    * A variable
    * A literal
    * A constant
    * All of the above

    <details>
    <summary>Reveal</summary>

    > All of the above

    </details>
    </details>

1.  <details>
    <summary>What is Type casting</summary>

    * The process of intialising a variable of a certain data type with a value
    * The process of declaring a variable with a datatype
    * The process of converting any datatype to string
    * The process of converting one datatype to another

    <details>
    <summary>Reveal</summary>

    > The process of converting one datatype to another

    Note that you cannot cast dissimilar types. You can't directly cast a number to a string or vice-versa (though there are library functions that perform this conversion). You can cast a numeric type to a different numeric type (e.g. int to float)

    </details>
    </details>

1.  <details>
    <summary>Select the correct statement to convert an integer to string</summary>

    1.  ```go
        var i int = 70
        str := strconv.Atoi(i)
        fmt.Println(str)
        ```

    1.  ```go
        var i int = 70
        str := fmt.Atoi(i)
        fmt.Println(str)
        ```

    1.  ```go
        var i int = 70
        str := strconv.Itoa(i)
        fmt.Println(str)
        ```

    1.  ```go
        var i int = 70
        str := fmt.Itoa(i)
        fmt.Println(str)
        ```

    <details>
    <summary>Reveal</summary>

    > C

    Know that string conversion functions are found in `strconv` package.

    Know that `Itoa` is so-named as it means "Integer to ASCII"

    </details>
    </details>

1.  <details>
    <summary>The package and function used for converting a string to integer is...</summary>

    * `fmt.toInteger()`
    * `strconv.Itoa()`
    * `fmt.Itoa()`
    * `strconv.Atoi()`

    <details>
    <summary>Reveal</summary>

    > `strconv.Atoi()`

    Following on from the previous question, we know that string conversions are found in `strconv` package. It logically follows that the name of the function is the opposite of what was the answer to the previous question.

    </details>
    </details>

1.  <details>
    <summary>Select the correct ways to convert an integer to float:</summary>

    1.  ```go
        var i int = 88
        f := float32(i)
        ```

    1.  ```go
        var i int = 88
        f := float64(i)
        ```

    1.  ```go
        var i int = 88
        f := float(i)
        ```

    1.  ```go
        var i int = 88
        f := float34(i)
        ```

    <details>
    <summary>Reveal</summary>

    > A, B

    Remember, there are two float types: `float32` and `float64`

    </details>
    </details>

