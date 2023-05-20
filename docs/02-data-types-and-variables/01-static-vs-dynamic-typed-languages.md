# Lab: Static vs Dynamic Typed Languages

[Take me to the lab!](https://kodekloud.com/topic/lab-introduction-to-go/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).

1.  <details>
    <summary>Which of the following languages are statically typed?</summary>

    1. Java
    2. C
    3. C++
    4. Python

    <details>
    <summary>Reveal</summary>

    > A, B, C

    </details>
    </details>

1.  <details>
    <summary>Which of the following languages are dynamically typed?</summary>

    1. C++
    2. Python
    3. Javascript
    4. PHP

    <details>
    <summary>Reveal</summary>

    > B, C, D

    </details>
    </details>

1.  <details>
    <summary>Choose the correct statements...</summary>

    1. Type checking process occurs at compile time for static typed languages.
    1. Type checking process occurs at runtime for static typed languages.
    1. Type checking process occurs at compile time for runtime typed languages.
    1. Type checking process occurs at runtime for dynamic typed languages.

    <details>
    <summary>Reveal</summary>

    > A, D

    </details>
    </details>

1.  <details>
    <summary>In dynamic typing, a variable is allowed to change its data type...</summary>

    * Depends on the data type
    * True
    * False
    * Only if it is an integer

    <details>
    <summary>Reveal</summary>

    > True

    </details>
    </details>

1.  <details>
    <summary>In static typing, a variable is allowed to change its data type...</summary>

    * Depends on the data type
    * True
    * False
    * Only if it is an integer

    <details>
    <summary>Reveal</summary>

    > False

    </details>
    </details>

1.  <details>
    <summary>A sample go program is stored under <b>/root/code/simple-project</b>. Inspect it.</br>What is the data type assigned to the variable called <b>title</b>?</summary>

    You can run this program from the integrated terminal like so

    ```bash
    cd simple-project
    go run main.go
    ```

    * `float`
    * `int`
    * `string`
    * `Sir`

    <details>
    <summary>Reveal</summary>

    > `string`

    Examine line 7 of the code.

    ```go
        title := "Sir"
    ````

    Recall that when `:=` is used to create a variable, the type of the new variable is inferred from what follows `:=`.<br/>`"Sir"` is a string constant, therefore the variable `title` will be of type `string`.

    </details>
    </details>


