# Lab: Recursive Functions

[Take me to the lab!](https://kodekloud.com/topic/lab-recursive-functions/)

Help for the [VSCode editor](https://github.com/kodekloudhub/community-faq/blob/main/docs/vscode-tips.md).

1.  <details>
    <summary>What is the most appropriate definition for recursion?</summary>

    1. A function that calls another function.
    1. A function that calls another execution instance of the same function.
    1. An in-built method for solving base cases related problems.
    1. A variadic function that calls another variadic function.

    <details>
    <summary>Reveal</summary>

    > B

    Also known as "a function that calls itself"

    </details>
    </details>

1.  <details>
    <summary>Complete the missing line (to calculate the factorial of a number)</summary>

    ```go
    func fact(n int) int {
        if n == 0 {
                return 1
        }
        return ______
    }
    ```

    <details>
    <summary>Reveal</summary>

    > `n * fact(n-1)`

    Calculating a factorial is a classic use case for recursion.

    ```
    n! = n * (n-1) * (n-2) * (n-3) * ... * 3 * 2 * 1
       = n * (n-1)!
    ```

    In mathematics, the factorial of a non-negative integer `n`, denoted by `n!`, is the product of all positive integers less than or equal to `n`. The factorial of `n` also equals the product of `n` with the next smaller factorial. This fact is what makes the calculation suitable for a recursive function.

    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    func print(n int) {
        if n == 0 {
                return
        }
        fmt.Print(n)
        print(n - 1)
    }

    func main() {
        print(5)
    }
    ```

    * 5 4 3 2 1
    * 54321
    * 12345
    * 1 2 3 4 5

    <details>
    <summary>Reveal</summary>

    > 54321

    * `main()` begins by calling `print()` with `5`.
    * In the `print()` function, `n` starts as `5`, so that is printed first. This eliminates two possible answers.
    * Then `print` calls itself, with `n-1`, i.e. 4. Here is the recursion.
    * `print` will keep doing this until `n == 0`, which will be after `1` has been printed. Then it will return all the way up and the program will end.
    * `fmt.Print` will not emit a space after printing an integer, so that leaves only the given answer.
`
    </details>
    </details>

1.  <details>
    <summary>What would be the output of the following program:</summary>

    ```go
    func print(n int) {
        if n == 0 {
                return
        }
        print(n - 1)
        fmt.Print(n)
    }

    func main() {
        print(5)
    }
    ```

    * 5 4 3 2 1
    * 54321
    * 12345
    * 1 2 3 4 5

    <details>
    <summary>Reveal</summary>

    > 12345

    This is subtly different from the previous question! Firstly for the same reason ias the previous question, we can rule out the answers that have spaces between the numbers.

    What's different? This time round it recurses all the way down until the function bottoms out (`n == 0`), then as it returns up the stack it prints the output. At maximum recursion it makes the fisrt return, then it starts printing where `n == 1` and returns and so on, so the numbers are printed in ascending order as we return up the stack.

    </details>
    </details>

1.  <details>
    <summary>Select the correct base case for function printSquares -</summary>

    for input n -> prints squares for n, n-1, n-2, ... -5

    Example: Input: n=2 Output: 4, 1, 0, 1, 4, 9, 16, 25

    ```go
    func print(n int) {
        // base case
        fmt.Printf("%d ", n*n)
        print(n - 1)
    }

    func main() {
        print(2)
    }
    ```

    Replace `// base case` with which of the following:

    *   ```go
        if n == 5 {
            return
        }
        ```
    *   ```go
        if n == -5 {
            return
        }
        ```
    *   ```go
        if n == 0 {
            return
        }
        ```
    *   ```go
        if n == -6 {
            return
        }
        ```

    <details>
    <summary>Reveal</summary>

    ```go
    if n == -6 {
        return
    }
    ```

    * The specification requires to print the squares of numbers from the starting value down to *and including* `-5`
    * The `print()` function prints the square first, then calls itself with the next smaller number
    * Therefore to get -5<sup>2</sup> printed, it will then call itself with -6, so this is what must be tested for to bottom out the recursion and return.

    </details>
    </details>



