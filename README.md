# Go for Beginners

Welcome to the world of Go! Whether you're just getting started or looking to refresh your knowledge, this guide will take you through the basics step by step.

## Hello World
Let's kick things off with the classic "Hello, World!" program. Open your Go file and type:

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

This simple program prints the famous greeting to the console.

## Variables
Go is statically typed, meaning you must declare the type of your variables. Here's an example:

```go
package main

import "fmt"

func main() {
    x := 5
    var y int = 10
    z := x + y
    fmt.Printf("Sum: %d\n", z)
}
```

Learn how to declare variables and perform basic arithmetic operations.

## Working With Strings
Strings in Go can be manipulated and combined. Explore string operations with this code:

```go
package main

import "fmt"

func main() {
    greeting := "Hello"
    name := "World"
    message := fmt.Sprintf("%s, %s!", greeting, name)
    fmt.Println(message)
}
```

## Working With Numbers
Perform operations on numbers in Go:
```go
package main

import "fmt"

func main() {
    a := 5
    b := 2
    sum := a + b
    product := a * b
    fmt.Printf("Sum: %d, Product: %d\n", sum, product)
}
```

## Getting Input From Users
Learn how to get user input with Go:

```go
package main

import "fmt"

func main() {
    var name string
    fmt.Println("Enter your name:")
    fmt.Scanln(&name)
    fmt.Printf("Hello, %s!\n", name)
}
```

## Arrays
Explore arrays in Go:

```go
package main

import "fmt"

func main() {
    numbers := [5]int{1, 2, 3, 4, 5}
    for _, num := range numbers {
        fmt.Printf("Number: %d\n", num)
    }
}
```

## Functions 
Define functions and call them:

```go
package main

import "fmt"

func add(x, y int) int {
    return x + y
}

func main() {
    result := add(3, 5)
    fmt.Printf("Sum: %d\n", result)
}
```

## For Loop
Iterate through a range of numbers:

```go
package main

import "fmt"

func main() {
    for i := 1; i <= 5; i++ {
        fmt.Printf("Number: %d\n", i)
    }
}
```

## While  Loop
Implement a simple while loop:

```go
package main

import "fmt"

func main() {
    count := 0
    for count < 5 {
        fmt.Printf("Count: %d\n", count)
        count++
    }
}
```

## Try / Except
Handle errors with Go's Result type:

```go
package main

import (
    "fmt"
    "strconv"
)

func main() {
    num, err := strconv.Atoi("42")
    if err == nil {
        fmt.Printf("Parsed number: %d\n", num)
    } else {
        fmt.Println("Failed to parse")
    }
}
```

## Reading Files
Read content from a file:

```go
package main

import (
    "fmt"
    "io/ioutil"
)

func main() {
    content, err := ioutil.ReadFile("example.txt")
    if err == nil {
        fmt.Printf("File content: %s\n", content)
    } else {
        fmt.Println("Failed to read the file")
    }
}
```

## Writing to Files
Write to a file in Go:

```go
package main

import (
    "fmt"
    "io/ioutil"
)

func main() {
    data := []byte("Hello, Go!")
    err := ioutil.WriteFile("output.txt", data, 0644)
    if err != nil {
        fmt.Println("Failed to write to the file")
    }
}
```

## Structs
Define a simple struct in Go:

```go
package main

import "fmt"

type Dog struct {
    Name string
    Age  uint8
}

func main() {
    myDog := Dog{
        Name: "Buddy",
        Age:  3,
    }

    fmt.Printf("Dog's name: %s\n", myDog.Name)
    fmt.Printf("Dog's age: %d\n", myDog.Age)
}
```

## Structs with Methods
While Go doesn't have traditional classes, you can achieve similar functionality with structs and methods:

```go
package main

import "fmt"

type Dog struct {
    Name string
    Age  uint8
}

func NewDog(name string, age uint8) Dog {
    return Dog{
        Name: name,
        Age:  age,
    }
}

func (d Dog) Bark() {
    fmt.Printf("%s says woof!\n", d.Name)
}

func main() {
    myDog := NewDog("Buddy", 3)
    myDog.Bark()
}
```

Feel free to explore more of Go's powerful features as you continue your learning journey! Happy coding!

# Practice Project

This simple Go project is designed for beginners to practice various language features. The program:

1. **User Input:**
   - Receives the user's name and age through standard input.

2. **Structs:**
   - Defines a `Person` struct to represent user data, including name and age.

3. **Basic Math Operations:**
   - Performs basic mathematical operations (sum, product, and square) on the user's age.

4. **Arrays:**
   - Stores the results of the mathematical operations in an array.

5. **File I/O:**
   - Writes both user information and operation results to a file named `output.txt`.

6. **Functions:**
   - Utilizes functions to modularize code for better organization and readability.

This project covers key Go concepts such as user input, structs, basic operations, arrays, file I/O, and functions. It serves as a practical hands-on exercise for those learning Go programming.

```go
package main

import (
	"fmt"
	"os"
	"strconv"
	"io/ioutil"
)

type Person struct {
	Name string
	Age  uint8
}

func main() {
	fmt.Println("Enter your name:")
	var name string
	fmt.Scanln(&name)

	fmt.Println("Enter your age:")
	var ageInput string
	fmt.Scanln(&ageInput)
	age, err := strconv.ParseUint(ageInput, 10, 8)
	if err != nil {
		fmt.Println("Invalid age. Using 0 as default.")
		age = 0
	}

	user := Person{Name: name, Age: uint8(age)}

	resultArray := performOperations(user.Age)

	welcomeMessage(user)

	writeToFile(user, resultArray)
}

func welcomeMessage(person Person) {
	fmt.Printf("Welcome, %s! You are %d years old.\n", person.Name, person.Age)
}

func performOperations(age uint8) []uint8 {
	sum := age + 5
	product := age * 2
	square := age * age

	fmt.Printf("Age + 5: %d\n", sum)
	fmt.Printf("Age * 2: %d\n", product)
	fmt.Printf("Age squared: %d\n", square)

	return []uint8{sum, product, square}
}

func writeToFile(person Person, results []uint8) {
	file, err := os.Create("output.txt")
	if err != nil {
		fmt.Println("Failed to create the file")
		return
	}
	defer file.Close()

	file.WriteString(fmt.Sprintf("Name: %s\nAge: %d\n\n", person.Name, person.Age))
	file.WriteString("Results:\n")

	for index, result := range results {
		file.WriteString(fmt.Sprintf("Operation %d: %d\n", index+1, result))
	}

	fmt.Println("The information has been written to the 'output.txt' file.")
}
```