# Lab: Pointers

[Take me to the lab!](https://kodekloud.com/topic/lab-pointers-in-functions/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).

1.  <details>
    <summary>What would be the output of the following program:</summary>

    Note: add package and import statements as needed

    ```go
    func modify(numbers ...int) {
        for i := range numbers {
                numbers[i] -= 5
        }
    }
    func main() {
        arr := []int{10, 20, 30}
        fmt.Println(arr)
        modify(arr...)
        fmt.Println(arr)
    }
    ```

    * [10 20 30]<br/>[5 15 25]
    * [10 20 30]<br/>[10 20 30]
    * [10 20 30]<br/>[15 25 35]
    * Error

    <details>
    <summary>Reveal</summary>

    > [10 20 30]<br/>[5 15 25]

    * Create a slice of `int` with 3 values
    * Print it
    * Call the function `modify` which takes a variadic argument. The slice is passed by reference, meaning that if it modifies the values in the slice, then the caller sees the change. Slice data is always passed by reference as they behave like pointers.
    * Hence in the final `Println` we see that 5 has bee subtracted from all values.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    Note: add package and import statements as needed

    ```go
    func modify(numbers [3]int) {
        for i := range numbers {
            numbers[i] -= 5
        }
    }
    func main() {
        arr := [3]int{10, 20, 30}
        fmt.Println(arr)
        modify(arr)
        fmt.Println(arr)
    }
    ```

    * [10 20 30]<br/>[5 15 25]
    * [10 20 30]<br/>[10 20 30]
    * [10 20 30]<br/>[15 25 35]
    * Error

    <details>
    <summary>Reveal</summary>

    > [10 20 30]<br/>[10 20 30]

    * This time an array has been declared, not a slice
    * Arrays are passed by value, therefore the `modify` function receives *a copy* of the array. The caller's array is not modified.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    Note: add package and import statements as needed

    ```go
    func modify(numbers *[3]int) {
        for i := range numbers {
                numbers[i] -= 5
        }
    }
    func main() {
        arr := [3]int{10, 20, 30}
        fmt.Println(arr)
        modify(arr)
        fmt.Println(arr)
    }
    ```

    * [10 20 30]<br/>[5 15 25]
    * [10 20 30]<br/>[10 20 30]
    * [10 20 30]<br/>[15 25 35]
    * Error

    <details>
    <summary>Reveal</summary>

    > Error

    * The program will not compile since the `modify` function expects a pointer to an array of `[3]int`.
    * The call `modify(arr)` is passing the array itself, not a pointer to it.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    Note: add package and import statements as needed

    ```go
    func modify(s *string) {
        *s = strings.ToUpper(*s)
    }

    func main() {
        s := "hello"
        fmt.Println(s)
        modify(&s)
        fmt.Println(s)
    }
    ```

    * hello HELLO
    * hello<br/>HELLO
    * HELLO hello
    * hello

    <details>
    <summary>Reveal</summary>

    > hello<br/>HELLO

    You must add `strings` as an import to use `ToUpper`

    * Initialize a string variable `s` with value `hello`, then print it.
    * The `modify` function takes a pointer to string, converts the value it is pointing to to upper case, then stores the conversion back in the variable being pointed to, i.e. it will modify the caller's variable.
    * `main` calls `modify` passing the address of the variable `s` - i.e. providing a pointer to `s`
    * Print the end result, which is now upper cased.
    * There is a newline in the output because `Println` was called twice and `Println` always appends a newline.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    Note: add package and import statements as needed

    ```go
    func modify(s map[string]int) {
        s["A"] = 100
    }
    func main() {
        ascii_codes := map[string]int{}
        ascii_codes["A"] = 65
        fmt.Println(ascii_codes)
        modify(ascii_codes)
        fmt.Println(ascii_codes)
    }
    ```

    * map[A:65]<br/>map[A:65]
    * map[A:65]<br/>map[A:100]
    * [A:65]<br/>[A:100]
    * [A:65]<br/>[A:65]

    <details>
    <summary>Reveal</summary>

    > map[A:65]<br/>map[A:100]

    * When a map is printed, it is always printed like `map[...]` so two answers can be ruled out immediately.
    * Maps are always passed by reference in function calls, therefore `modify` will modify the `ascii_codes` map and the modification is seen in the second print.

    </details>
    </details>

*   <details>
    <summary>Wrap up</summary>

    * Slices and maps are always passed by reference so they behave like pointers to the caller's data when used as function arguments. If a function modifies a slice or a map argument, the change will affect the caller.
    * All other types, including arrays are passed by value (a copy is made for the function to use). If you want a function to be able to modify the caller's variable, then you must use a function that takes a pointer argument like Q4, and pass the address of your variable (`&` operator) to the function.
    * When using or modifying the value being pointed to in the function, you use the dereference operator (`*`).

    </details>
