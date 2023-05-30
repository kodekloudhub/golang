# Lab: Interfaces

[Take me to the lab!](https://kodekloud.com/topic/lab-interfaces/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).

1.  <details>
    <summary>Select the correct declarations for an interface.</summary>

    1.  ```go
        type Student interface {
            id int
            grades  []int
            func calcGrades()
        }
        ```
    1.  ```go
        type Student interface {
            calcGrades()
            getName()
        }
        ```
    1.  ```go
        type Employee interface {
            calcSalary()
            getName()
        }
        ```
    1.  ```go
        type Employee interface {
            func calcSalary()
            func getName()
        }
        ```

    <details>
    <summary>Reveal</summary>

    > B, C

    * A is incorrect because interfaces cannot have fields, only methods.
    * D is incorrect because the `func` keyword is not used on interface method declarations.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program?</summary>

    Note: add package and import statements as needed

    ```go
    type Student interface {
        getPercentage() int
        getName()
    }

    type Undergrad struct {
        name   string
        grades []int
    }

    func (u Undergrad) getPercentage() int {
        sum := 0
        for _, v := range u.grades {
            sum += v
        }
        return sum / len(u.grades)
    }

    func printPercentage(s Student) {
        fmt.Println(s.getPercentage())
    }

    func main() {
        grades := []int{90, 75, 80}
        u := Undergrad{"Ross", grades}
        printPercentage(u)
    }
    ```

    * No output
    * Error
    * 81
    * 81%

    <details>
    <summary>Reveal</summary>

    > Error

    * There is a bug in this program. It will fail to compile due to the last line which will produce the error `Undergrad does not implement Student (missing getName method)`
    * When a struct value is passed as an argument to a function that has an interface parameter, the struct's implementation will be checked by the compiler.
    * `Undergrad` has a receiver for `getPercentage` but not for `getName` therefore it is an incomplete implementation of the interface `Student`.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program?</summary>

    Note: add package and import statements as needed

    ```go
    type Student interface {
        getPercentage() int
        getName() string
    }

    type Undergrad struct {
        name   string
        grades []int
    }

    func (u Undergrad) getPercentage() int {
        sum := 0
        for _, v := range u.grades {
            sum += v
        }
        return sum / len(u.grades)
    }
    func (u Undergrad) getName() string {
        return u.name
    }

    func printData(s Student) {
        fmt.Println(s.getName())
        fmt.Println(s.getPercentage())
    }

    func main() {
        grades := []int{90, 75, 80}
        u := Undergrad{"Ross", grades}
        printData(u)
    }
    ```

    * No output
    * Ross<br/>81
    * Error
    * 81<br/>Ross

    <details>
    <summary>Reveal</summary>

    > Ross<br/>81

    * The bug from Q2 has been fixed. An implementation has been provided for `getName`, so no error.
    * `No output` is incorrect because the two `Println` statements in the `printData` function will be executed.
    * While we're there, note that the name will be printed first, so that eliminates another answer.
    * Finally, `getPercentage` calculates the average of all the grades in the `grades` slice. The calculation is using integer math, hence `81`. No percent sign is printed.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program?</summary>

    Note: add package and import statements as needed

    ```go
    type Student interface {
        getPercentage() int
        getName() string
    }

    type Undergrad struct {
        name   string
        grades []int
    }

    type Postgrad struct {
        name   string
        grades []int
    }

    func (p Postgrad) getPercentage() int {
        sum := 0
        for _, v := range p.grades {
            sum += v
        }
        return ((sum * 100) / (len(p.grades) * 200))
    }
    func (p Postgrad) getName() string {
        return p.name
    }

    func (u Undergrad) getPercentage() int {
        sum := 0
        for _, v := range u.grades {
            sum += v
        }
        return sum / len(u.grades)
    }

    func (u Undergrad) getName() string {
        return u.name
    }

    func printData(s Student) {
        fmt.Println(s.getName())
        fmt.Println(s.getPercentage())
    }

    func main() {
        u := Undergrad{"Ross", []int{90, 75, 80}}
        p := Postgrad{"Joe", []int{150, 190, 185}}
        printData(u)
        printData(p)
    }
    ```

    * Ross 81<br/>Joe 87
    * Joe 87<br/>Ross 81
    * Ross<br/>81<br/>Joe<br/>87
    * Ross<br/>Joe<br/>81<br/>87

    <details>
    <summary>Reveal</summary>

    > Ross<br/>81<br/>Joe<br/>87

    * Now there is a new struct `Postgrad`. `Postgrad` correctly implements the `Student` interface as it has correct receivers for `getName` and `getPercentage`.
    * Note that the `getPercentage` for `Postgrad` is a different implementation, i.e. the percentage is calculated differently.
    * The function `printData` is the same as in Q3, therefore from that we know the order in which it will print the student data (name, newline, percentage). This eliminates two answers. It also eliminates a third because it won't output two names followed by two percentages.


    </details>
    </details>

1.  <details>
    <summary>Which of the following keyword is used to implement an interface in Golang?</summary>

    * type struct
    * receiver
    * No keyword needed to implement an interface
    * type interface

    <details>
    <summary>Reveal</summary>

    > No keyword needed to implement an interface

    * Keywords are used to *declare* an interface, not *implement* it.
    * Implementation is achieved by providing all of the correct receiver methods as defined by the interface for any struct that wants to provide an implementation.

    </details>
    </details>

