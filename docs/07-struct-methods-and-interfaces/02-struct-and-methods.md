# Lab: Struct and Methods

[Take me to the lab!](https://kodekloud.com/topic/lab-struct-and-methods/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).

Methods are special functions that operate on structs or pointers to structs. They are also known as `receivers`. This, along with interfaces is as close as Go gets to Object Oriented Programming (OOP).

1.  <details>
    <summary>What would be the output of the following program?</summary>

    Note: add package and import statements as needed

    ```go
    type Movie struct {
            name    string
            summary string
            rating  float32
    }

    func (m Movie) getSummary() {
            m.summary = "summary"
    }

    func (m *Movie) increaseRating() {
            m.rating += 1
    }

    func main() {
            mov := Movie{"xyz", "", 2.1}
            fmt.Printf("%+v", mov)
            mov.increaseRating()
            mov.getSummary()
            fmt.Printf("%+v", mov)
    }
    ```

    * {name:xyz summary: rating:2.1}{name:xyz summary: rating:3.1}
    * {name:xyz summary:summary rating:2.1}<br/>{name:xyz summary:summary rating:3.1}
    * {name:xyz summary:summary rating:2.1}{name:xyz summary:summary rating:3.1}
    * {name:xyz summary: rating:2.1}<br/>{name:xyz summary: rating:3.1}

    <details>
    <summary>Reveal</summary>

    > {name:xyz summary: rating:2.1}{name:xyz summary: rating:3.1}

    Our old friend the `Movie` struct reappears, this time with an additional field `summary` and a couple of methods.

    * We can immediately rule out any answer that has a newline between the two outputs, as `Printf` does not emit newline unless the format string contains `\n`.
    * So why was the summary not set in the call to `getSummary`? Notice that this method is not a pointer receiver, therefore setting values in the struct will have no effect on the caller.
    * However `increaseRating` *is* a pointer receiver, therefore the caller's variable `mov` is modified.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program?</summary>

    Note: add package and import statements as needed

    ```go
    type Rectangle struct {
        length  int
        breadth int
    }

    func (r Rectangle) area() int {
        return r.length * r.breadth
    }

    func main() {
        r := Rectangle{breadth: 10, length: 5}
        fmt.Println(r.area())
        fmt.Println(r)
    }
    ```

    * 50<br/>{10 5}
    * 0<br/>{5 10}
    * 50<br/>{5 10}
    * 0<br/>{10 5}

    <details>
    <summary>Reveal</summary>

    > 50<br/>{5 10}

    * From the final `Println` where we print `r`, the rectangle struct, we can immediately rule out any answer that prints `{10, 5}` as the fields in the struct are printed in the order they appear in the `type` declaration for the struct.
    * Where we initialize the struct in the first line of `main()`, the field initializers when naming the fields can be listed in any order.
    * We have a non-pointer receiver `area` which simply returns the area of the rectangle. We are not setting fields in the rectangle struct so we don't require a pointer receiver.
    * The first `Println` prints the value returned from the `area` call, which is `50`, yielding the correct answer.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program?</summary>

    Note: add package and import statements as needed

    ```go
    type Rectangle struct {
        length  int
        breadth int
    }

    func (r Rectangle) area() int {
        return r.length * r.breadth
    }

    func (r *Rectangle) incLength(n int) {
        for i := 0; i < n; i++ {
            r.length += i
        }
    }

    func main() {
        r := Rectangle{breadth: 10, length: 5}
        fmt.Println(r.area())
        fmt.Println(r)
        r.incLength(7)
        fmt.Println(r.area())
        fmt.Println(r)
    }
    ```

    * error
    * 50 {5 10}<br/>260 {26 10}
    * 50<br/>{5 10}<br/>50<br/>{26 10}
    * 50<br/>{5 10}<br/>260<br/>{26 10}

    <details>
    <summary>Reveal</summary>

    > 50<br/>{5 10}<br/>260<br/>{26 10}

    * The program compiles and has no pointer bugs, so no error.
    * There are four separate `PrintLn` so anything that is not four lines of output can be eliminated.
    * We have the same struct, it's initialized the same way as the previous question, and the same `area` receiver.
    * There is an additional *pointer* receiver `incLength` which can modify fields in the struct.
    * The first `Println` for `area` and the following `Println` for the structure will give the same output as the previous question.
    * Next, we call `incLength` with `7`. That will add incrementing values of `i` in the `for` loop to the length, i.e. 0 then 1, then 2 all the way up to 6, therefore length ends up as `26`.
    * Print the area and the struct again, which now has the modified length of `26`

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program?</summary>

    Note: add package and import statements as needed

    ```go
    type Employee struct {
        eid int
        id  int
    }

    func main() {
        employees := make([]Employee, 5)
        for i := range employees {
            employees[i] = Employee{i, i + 10}
            fmt.Println(employees[i])
        }
    }
    ```

    * error
    * {eid:0 id:10}<br/>{eid:1 id:11}<br/>{eid:2 id:12}<br/>{eid:3 id:13}<br/>{eid:4 id:14}
    * {0 10}<br/>{1 11}<br/>{2 12}<br/>{3 13}<br/>{4 14}
    * {0 }<br/>{1 }<br/>{2 }<br/>{3 }<br/>{4 }

    <details>
    <summary>Reveal</summary>

    > {0 10}<br/>{1 11}<br/>{2 12}<br/>{3 13}<br/>{4 14}

    * There's no error
    * We can rule out any answer that prints the field names, because `Println` won't do that
    * We can also rule out any answer that does not include two values in each `{}` since both fields are `int` and `int` always has a printable value, even if it's zero.
    * This leaves only one answer. The reason it has the values it does, is because we initialize each value in the struct without giving the field names, so the values are applied in order: `eid` first, then `id`. The `eid` values will go from zero to 4, and the `id` being `i+10` will go from 10 to 14.

    It is however good practice to use field names when initializing a struct since it makes the code easier to read.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program?</summary>

    Note: add package and import statements as needed

    ```go
    type Employee struct {
        eid int
        id  int
    }

    func (e Employee) get_id() int {
        return e.eid + 10
    }

    func main() {
        employees := make([]Employee, 5)
        for i := range employees {
            employees[i] = Employee{eid: i}
            employees[i].id = employees[i].get_id()
            fmt.Printf("%+v\n", employees[i])
        }
    }
    ```

    * {0 0}<br/>{1 0}<br/>{2 0}<br/>{3 0}<br/>{4 0}
    * {eid:0 id:0}<br/>{eid:1 id:0}<br/>{eid:2 id:0}<br/>{eid:3 id:0}<br/>{eid:4 id:0}
    * {0 10}<br/>{1 11}<br/>{2 12}<br/>{3 13}<br/>{4 14}
    * {eid:0 id:10}<br/>{eid:1 id:11}<br/>{eid:2 id:12}<br/>{eid:3 id:13}<br/>{eid:4 id:14}

    <details>
    <summary>Reveal</summary>

    > {eid:0 id:10}<br/>{eid:1 id:11}<br/>{eid:2 id:12}<br/>{eid:3 id:13}<br/>{eid:4 id:14}

    * We can rule out any answer that does not print the field names, because we are using `%+v` formatter.
    * There is a receiver `get_id` that returns the current value of `eid` plus 10
    * In the for loop, each struct is initialized with a value for `eid` only
    * Then the `id` is set with the value returned by `get_id`, i.e the `eid` plus ten, which means that `id` is not going to be zero when the struct is printed.
    * Then print the struct.

    </details>
    </details>

