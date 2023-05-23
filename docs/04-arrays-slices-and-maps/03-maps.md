# Lab: Maps

[Take me to the lab!](https://kodekloud.com/topic/lab-maps/)

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
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            var ascii_codes map[string]int
            ascii_codes["A"] = 65
            fmt.Println(ascii_codes)
    }
    ```

    * A => 65
    * map[]
    * map[A:65]
    * Error

    <details>
    <summary>Reveal</summary>

    > Error

    The program will compile and run, however it will panic because the map is `nil` and can't be assigned to.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            ascii_codes := map[string]string{}
            ascii_codes["A"] = 65
            fmt.Println(ascii_codes)
    }
    ```

    * A => 65
    * map[]
    * map[A:65]
    * Error

    <details>
    <summary>Reveal</summary>

    > Error

    This time the program will fail to compile. Compile time type checking spots that we are trying to add an integer value to a map that expects string values.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            ascii_codes := map[string]int{}
            ascii_codes["A"] = 65
            _, found := ascii_codes["B"]
            if found {
                    fmt.Println("key B was not found")
            }
    }
    ```

    * No output
    * A => 65
    * key B was not found
    * Error

    <details>
    <summary>Reveal</summary>

    > No output

    * Key B was indeed not found, therefore the variable `found` is `false`. The logic to get to the `Println` requires `found` to be true.

    Note that this is a contrived example. In reality such code would be a developer bug!

    </details>
    </details>

1.  <details>
    <summary>Follow the given steps and select the correct output</summary>

    Let's write the program according to the specification in the question

    ```go
    package main

    import "fmt"

    func main() {
        // create a map using make() function with key data type as string, and value data type as int.
        ascii_codes := make(map[string]int)
        // Add the give key-value pairs
        ascii_codes["A"] = 65
        ascii_codes["F"] = 70
        ascii_codes["K"] = 75
        // Delete the key "F"
        delete(ascii_codes, "F")
        // Print the map
        fmt.Println(ascii_codes)
    }
    ```

    What is the correct output?

    * Error
    * A => 65
    * A => 65</br>B => 75
    * map[A:65 K:75]

    <details>
    <summary>Reveal</summary>

    > map[A:65 K:75]

    This format is how `Println` prints maps. We have deleted the "F" entry, so only have the two other values.

    </details>
    </details>

1.  <details>
    <summary>Follow the given steps and select the correct output:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            ascii_codes := make(map[string]int)
            ascii_codes["A"] = 65
            ascii_codes["F"] = 70
            ascii_codes["K"] = 75
            fmt.Println(ascii_codes)

            ascii_codes = make(map[string]int)
            ascii_codes["U"] = 85
            fmt.Println(ascii_codes)
    }
    ```

    * map[A:65 F:70 K:75 U:85]
    * map[A:65 F:70 K:75]<br/>map[U:85]
    * map[A:65 F:70 K:75]<br/>map[A:65 F:70 K:75 U:85]
    * Runtime Error

    <details>
    <summary>Reveal</summary>

    > map[A:65 F:70 K:75]<br/>map[U:85]

    * A map with 3 entries is created then printed.
    * Then the variable `ascii_codes` is overwritten with a *new* map that has the single entry for `U`. The original map is discarded.

    </details>
    </details>

1.  <details>
    <summary>Follow the given steps and select the correct output:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            ascii_codes := make(map[string]int, 10)
            ascii_codes["A"] = 65
            ascii_codes["F"] = 70
            ascii_codes["K"] = 75
            fmt.Println(len(ascii_codes))
            ascii_codes = make(map[string]int)
            ascii_codes["U"] = 85
            fmt.Println(len(ascii_codes))
    }
    ```
    * 3<br/>4
    * 3<br/>1
    * Runtime Error
    * 3<br/>3

    <details>
    <summary>Reveal</summary>

    > 3<br/>1

    * The second argument to `make` for maps is *initial capacity*, not length. Because only 3 values are added, `len()` returns 3.
    * The map is recreated and one entry added to it, so the second call to `len()` yields 1.
    </details>
    </details>
