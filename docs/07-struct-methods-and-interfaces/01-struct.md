# Lab: Struct

[Take me to the lab!](https://kodekloud.com/topic/lab-struct/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).

1.  <details>
    <summary>What would be the output of the following program?</summary>

    Note: add package and import statements as needed

    ```go
    type Movie struct {
        name   string
        rating float32
    }

    func main() {
        m := Movie{name: "ABCD"}
        var m2 Movie
        fmt.Printf("%+v", m)
        fmt.Printf("%+v", m2)
    }
    ```

    * {name: rating:0}{name: rating:0}
    * {name:ABCD rating:0}{name: rating:0}
    * error
    * {name:ABCD rating:0}

    <details>
    <summary>Reveal</summary>

    > {name:ABCD rating:0}{name: rating:0}

    * We have a struct `Movie` with two fields, one `string` and one `float32`.
    * Initialize variable `m` with a `Movie` value setting only the `name` field.
    * Initialize variable `m2` with a `Movie`, not settings any of the fields.
    * Know that all fields of a struct will be initialized with the default values for the fields types if they are not explicitly set, so `string` fields get empty string and `float32` (like all numerics) get zero.
    * Now print `m`. The `%+v` formatter means include the field names and field values. So this will emit `{name:ABCD rating:0}` because we set the name in `m`. No newline will be printed since we did not put a `\n` in the string to be printed. Remember only `Println` automatically outputs a newline.
    * Now print `m2` which did not have any fields set, so that emits `{name: rating:0}`

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program?</summary>

    Note: add package and import statements as needed

    ```go
    type Movie struct {
        name   string
        rating float32
    }

    func getMovie(s string, r float32) (m Movie) {
        m = Movie{
            name:   s,
            rating: r,
        }
        return
    }

    func main() {
        fmt.Printf("%+v", getMovie("xyz", 3.5))
    }
    ```

    * {name: rating:0}
    * {name:xyz rating:3.5}
    * {xyz 3.5}
    * error

    <details>
    <summary>Reveal</summary>

    > {name:xyz rating:3.5}

    * We have the same struct as the previous question.
    * We have a new function `getMovie` that initializes a `Movie` struct and returns it using named return value `m`
    * Call the function with `xyz` and `3.5` as arguments. These will be put into the struct.
    * Print the return value (i.e. the initialized struct) with `%+v` formatter.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program?</summary>

    Note: add package and import statements as needed

    ```go
    func getMovie(s string, r float32) (m Movie) {
        m = Movie{
                name:   s,
                rating: r,
        }
        return
    }

    func increaseRating(m *Movie) {
        m.rating += 1.0
    }

    func main() {
        mov := getMovie("xyz", 2.0)
        increaseRating(mov)
        fmt.Printf("%+v", mov)
    }
    ```

    * xyz<br/>3
    * error
    * {xyz 3}
    * {name:xyz rating:3}

    <details>
    <summary>Reveal</summary>

    > Error

    The program will fail to compile because there is a bug!

    The function `increaseRating` requires a pointer to `Movie` struct so that it can modify the values within. In the call to `increaseRating`, the address of `mov` should have been passed, i.e. needs to be `increaseRating(&mov)`

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program?</summary>

    Note: add package and import statements as needed

    ```go
    type Movie struct {
        name   string
        rating float32
    }

    func getMovie(s string, r float32) (m Movie) {
        m = Movie{
                name:   s,
                rating: r,
        }
        return
    }

    func main() {
        mov := getMovie("xyz", 2.0)
        fmt.Println(mov.name)
        fmt.Println(mov.ratings)
    }
    ```

    * xyz 2
    * xyz<br/>2
    * name: xyz<br/>rating: 2
    * error

    <details>
    <summary>Reveal</summary>

    > Error

    The program will fail to compile because there is another bug!

    In the last line of the program it is trying to print `mov.ratings`. `Movie` struct has no field `ratings`. The correct name is `rating`.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program?</summary>

    Note: add package and import statements as needed

    ```go
    type Movie struct {
        name   string
        rating float32
    }

    func getMovie(s string, r float32) (m Movie) {
        m = Movie{
            name:   s,
            rating: r,
        }
        return
    }

    func main() {
        mov := getMovie("xyz", 2.1)
        mov1 := getMovie("abc", 3.3)
        movies := make([]Movie, 5)
        movies = append(movies, mov)
        movies = append(movies, mov1)
        for _, value := range movies {
            fmt.Println(value)
        }
    }
    ```

    * { 0}<br/>{ 0}<br/>{ 0}<br/>{ 0}<br/>{ 0}<br/>{xyz 2.1}<br/>{abc 3.3}
    * { 0}<br/>{ 0}<br/>{ 0}<br/>{ 0}<br/>{ 0}<br/>{xyz 2}<br/>{abc 3}
    * {name:xyz rating:2.1}<br/>{name:abc rating:3.3}<br/>{name: rating:0}<br/>{name: rating:0}<br/>{name: rating:0}<br/>{name: rating:0}<br/>{name: rating:0}
    * {name: rating:0}<br/>{name: rating:0}<br/>{name: rating:0}<br/>{name: rating:0}<br/>{name: rating:0}<br/>{name:xyz rating:2.1}<br/>{name:abc rating:3.3}

    <details>
    <summary>Reveal</summary>

    > { 0}<br/>{ 0}<br/>{ 0}<br/>{ 0}<br/>{ 0}<br/>{xyz 2.1}<br/>{abc 3.3}

    * Two movie structs are initialized using the `getMovie` function. Both are given ratings with a floating point number. This rules out the second answer above as a possibility since its ratings are integers.
    * Next, a slice of 5 `Movie` structs is created. All five will be initialized as per the rules mentioned in the explanation for Q1.
    * Now we *append* `mov` and `mov1` to the slice, so these will appear *following* the five empty movies.
    * When the slice is iterated with `range` the five empty ones will come first, then `mov` then `mov1`. This rules out any answer where `mov` and `mov1` are printed first.
    * The default formatter for `Println` is `%v` therefore field names will not be printed, only values, so that rules out any answer where the words "name" and "rating" are printed, leaving only the one possible answer.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program?</summary>

    Note: add package and import statements as needed

    ```go
    type Movie struct {
        name   string
        rating float32
    }

    func main() {
        mov := Movie{"xyz", 2.1}
        mov1 := Movie{"abc", 2.1}
        if mov.rating == mov1.rating || mov != mov1 {
            fmt.Println("condition met")
        } else if mov.rating == mov1.rating {
            fmt.Println("condition_2 met")
        }
    }
    ```

    * error
    * no output
    * condition met<br/>condition_2 met
    * condition met

    <details>
    <summary>Reveal</summary>

    > condition met

    * Initialize two movies. They have different names but the same rating.
    * `mov.rating == mov1.rating` is true. What comes after `||` doesn't matter and won't be evaluated because the left hand side of `||` was true. However the second condition is in fact true. The two movies are not equal because they have different names. Even if it was false, it would have no effect and `condition met` would still be printed.
    * The `else if` clause is also true, but it will not be executed because the first `if` was true.

    </details>
    </details>

