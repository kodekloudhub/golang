# Lab: Constants

[Take me to the lab!](https://kodekloud.com/topic/lab-constants/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).

1.  <details>
    <summary>A constant is initialised using the keyword:</summary>

    * `var`
    * `fixed_var`
    * `const`
    * `constant`

    <details>
    <summary>Reveal</summary>

    > `const`

    </details>
    </details>

1.  <details>
    <summary>Select the valid statements for declaring and initialising a constant</summary>

    1. `const c int = "mouse"`
    1. `const c int = 90`
    1. `const c = 90`
    1. `const c int = 90.00`

    <details>
    <summary>Reveal</summary>

    > B, C

    A and D are type mismatches.

    </details>
    </details>

1.  <details>
    <summary>Select the correct statements</summary>

    1.  ```go
        const c int = 70
        ```

    1.  ```go
        const c int
        c = 70
        ```

    1.  ```go
        var c int
        c = 70
        ```

    1.  ```go
        var c = 90
        ```

    <details>
    <summary>Reveal</summary>

    > A, C, D

    B is incorrect because a `const` must be assigned a value when it is declared, not in a separate statement.

    </details>
    </details>

1.  <details>
    <summary>Can you use shorthand declaration for declaring constants (:=)</summary>

    * No
    * Yes
    * Optional
    * None of the above

    <details>
    <summary>Reveal</summary>

    > No

    </details>
    </details>

1.  <details>
    <summary>Which of the following statement will throw an error</summary>

    1.  ```go
        const name = "Harry"
        fmt.Print(name)
        ```

    1.  ```go
        var name = "Harry"
        fmt.Print(name)
        ```

    1.  ```go
        const name = "Harry"
        name = "Snape"
        fmt.Print(name)
        ```

    1.  ```go
        var name string = "Harry"
        fmt.Print(name)
        ```

    <details>
    <summary>Reveal</summary>

    > C

    `const` is by definition constant. This means that once declared, it cannot be reassigned.

    </details>
    </details>

