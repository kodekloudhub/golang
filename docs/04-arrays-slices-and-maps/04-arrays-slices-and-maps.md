# Lab: Arrays, Slices and Maps

[Take me to the lab!](https://kodekloud.com/topic/lab-arrays-slices-and-maps/)

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
            arr := [5]string{"one", "two", "three"}
            slice := arr[:3]
            my_map := make(map[int]string)
            for i, el := range slice {
                    my_map[i+1] = el
            }
            fmt.Println(my_map)
    }
    ```

    * map[1:one 2:two 3:three]
    * Syntax Error
    * map["1":one "2":two "3":three]
    * 1 => one<br/>2 => two

    <details>
    <summary>Reveal</summary>

    > map[1:one 2:two 3:three]

    There's no syntax error in this program, so that answer is eliminated. The program flows like this:

    1. Create an array of 5 strings. Set values for the first 3
    1. Create a slice over the first 3 elements of the array
    1. Make a new map with integer keys and string values (eliminates answer `map["1":one "2":two "3":three]`).
    1. Use `for` to iterate the slice, getting index in `i` and value in `el`
        1. Add a map entry with key of `i+1` and value taken from the slice at position `i`. This will result in keys of 1, 2, 3 and corresponding values of one, two, three
    1. Print the map


    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            arr := [5]int{}
            my_map := make(map[string]int)
            my_map["A"] = 65
            my_map["B"] = 66
            i := 0
            for _, value := range my_map {
                    arr[i] = value
                    i += 1
            }
            fmt.Println(arr)
    }
    ```

    * [A B ]
    * [65 66 0 0 0]
    * Runtime Error
    * [65 66 67 0 0]

    <details>
    <summary>Reveal</summary>

    > [65 66 0 0 0]

    The program flows like this:

    1. Create an array of 5 ints. Recall that all 5 elements in the array will be initialized with the default value of int - zero.
    1. Make a new map with string keys and int values.
    1. Create two keys A and B with corresponding values 1 and 2 in the map.
    1. Set index variable `i` to zero.
    1. Use `for` to iterate the map values only. The keys are ignored with `_`.
        1. Set the array element at index `i` with the value received from the map.
        1. Increment `i` ready for next array element.
    1. Print the array.

    We can eliminate `Runtime Error` as an answer as the only place that could occur is in the `for` loop if we exceeded the size of the array. The `for` loop will iterate 2 map elements. The array will fit 5 values.

    The two values from the map will be stored in the first two elements of the array, yielding the given answer.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            arr := [5]int{10, 20, 30, 90, 100}
            new_slice := append(arr[:3], arr[4:]...)
            fmt.Print(new_slice)
    }
    ```

    * [10 20 90 100]
    * [10 20 30 90]
    * [10 20 30 100]
    * [10, 20, 30, 90, 100]

    <details>
    <summary>Reveal</summary>

    > [10 20 30 100]

    The program flows like this:

    1. Create an array of 5 ints, all with initial values
    1. Create a new slice by taking the first 3 elements of `arr` (10, 20, 30) and appending the rest of `arr` from element 4 to the end (100).
    1. Print the slice, yielding the given answer.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            my_map := make([int]int)
            my_map[2] = 4
            my_map[4] = 16
            my_map[8] = 64
            delete(my_map, 4)
            fmt.Print(my_map)
    }
    ```

    * map[2:4 4:16]
    * map[2:4 8:64]
    * map[8:64 4:16]
    * Error

    <details>
    <summary>Reveal</summary>

    > Error

    The program will not compile because `make([int]int)` is a syntax error. Should have been `make(map[int]int)`.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    package main

    import "fmt"

    func main() {
            arr := [10]string{"a", "b", "c"}
            hashmap := make(map[string]int)
            my_slice := arr[:]
            fmt.Println(len(my_slice))
            fmt.Println(cap(my_slice))
            fmt.Println(len(hashmap))
    }
    ```

    * 3<br/>10<br/>1
    * 1<br/>10<br/>1
    * Error
    * 10<br/>10<br/>0

    <details>
    <summary>Reveal</summary>

    > 10<br/>10<br/>0

    The program flows like this:

    1. Create an array of 10 strings with values for the first 3. The remaining 7 elements will have the default value for string with is the empty string.
    1. Make a new map with string keys and integer values.
    1. Make a slice over `arr`. Note that `[:]` means include *all* elements, in this case 10.
    1. Print len of `my_slice` - will be 10 as noted in the point above.
    1. Print cap of `my_slice` - will also be 10 as we included the whole array.
    1. Print len of `hashmap` - will be zero because we added no map entries.

    </details>
    </details>

