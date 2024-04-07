# Learn Go

## Resources
- [Learn GO by Alex Mux](https://www.youtube.com/watch?v=8uiZC0l4Ajw&t=255s)
- [Golang Project Layout](https://github.com/golang-standards/project-layout)

## Six Main Points
1. Statically Typed Language
2. Strongly Typed Language
3. GO is Compiled
4. Fast Compile Time
5. Built in Concurrency (Goroutines)
6. Simplicity

## Difference between Modules and Packages
- Package: Dir that contains a collection of go files
- Module: Collection of Packages
- When we intialize a project we are intializing a module

## How to start a project
```bash
go mod init <github repo link>
go mod init go_tutorials # example
```
- This will generate go.mod file contents version no. and external mod
```
module go_tutorials

go 1.21.5
```

## Create a go file
- Every go file is a part of package
- Package mush be same for all the files in a dir
- `packege main` is the file with entry point of the code

## Running a go program
```bash
go build cmd/tutorial_1/main.go
go run cmd/tutorial_1/main.go
```

## Data Types
```go
package main


import (
	"fmt"
	"unicode/utf8"
)

func main() {
  var intNum int = 32767
  intNum = intNum + 1
  fmt.Println(intNum)

  var floatNum float64 = 12345678.9
  fmt.Println(floatNum)

  var floatNum32 float32 = 10.1
  var intNum32 int32 = 2
  var result float32 = floatNum32 + float32(intNum32)
  fmt.Println(result)

  var intNum1 int = 3
  var intNum2 int = 2
  fmt.Println(intNum1 / intNum2)
  fmt.Println(intNum1 % intNum2)

  var myString1 string = "Hello World"
  var myString2 string = `Hello
  World
  `
  fmt.Println(myString1)
  fmt.Println(myString2)

  
  var myString string = "Hello" + " " + "World"
  fmt.Println(myString)


  fmt.Println(len("test")) // returns the no. of bytes 

  fmt.Println(utf8.RuneCountInString("γ"))
  
  var myRune rune = 'a'
  fmt.Println(myRune)

  var myBoolean bool = false
  fmt.Println(myBoolean)


  var intNum3 int 
  fmt.Println(intNum3)

  myVar := "text"
  fmt.Println(myVar)

  var1, var2 := 1, 2
  fmt.Println(var1, var2)

  const myConst string = "const value"
  fmt.Println(myConst)
}
```

## Functions and Control Structure
```go
package main

import (
  "errors"
  "fmt"
)

func main() {
  var printValue string = "Hello World"
  printMe(printValue)

  var numerator int = 11
  var denominator int = 0
  var result, remainder, err = intDivision(numerator, denominator)
  if err != nil {
    fmt.Printf(err.Error())
  } else if remainder == 0 {
    fmt.Printf("The result of the integer division is %v", result)
  } else {
    fmt.Printf("The result of the integer division is %v with remainder %v", result, remainder)
  }

  switch {
  case err != nil:
    fmt.Printf(err.Error())
  case remainder == 0:
    fmt.Printf("The result of the integer division is %v", result)
  default:
    fmt.Printf("The result of the integer division is %v with remainder %v", result, remainder)
  }

  switch remainder {
  case 0:
    fmt.Printf("The division was exact")
  case 1, 2:
    fmt.Printf("The division was close")
  default:
    fmt.Printf("The division was not close")
  }

}

func printMe(printValue string) {
  fmt.Println(printValue)
}

func intDivision(numerator int, denominator int) (int, int, error) {
  var err error // default value is nil
  if denominator == 0 {
    err = errors.New("Cannot Divide by Zero")
    return 0, 0, err
  }
  return numerator / denominator, numerator % denominator, err 
}
```

## Array, Slices, Maps and Loops
```go
package main

import "fmt"

/*
[]Arrays
- Fixed Length
- Same Type
- Indexable
- Contiguous in Memory

[]Slice
- Similar to vector
- Can be expaned later

map[string]int32
- key value pair
*/

func main() {
  var intArr [3]int32
  intArr[1] = 124
  fmt.Println(intArr[0])
  fmt.Println(intArr[1:3])

  fmt.Println(&intArr[0])
  fmt.Println(&intArr[1])
  fmt.Println(&intArr[2])

  var intArr2 [3]int32 = [3]int32{1, 2, 3}
  // intArr2 := [...]int32{1, 2, 3}
  fmt.Println(intArr2)

  var intSlice []int32 = []int32{4, 5, 6}
  fmt.Println(intSlice)
  fmt.Printf("The length is %v with capacity %v\n", len(intSlice), cap(intSlice))

  intSlice = append(intSlice, 7)
  fmt.Println(intSlice)
  fmt.Printf("The length is %v with capacity %v\n", len(intSlice), cap(intSlice))

  var intSlice2 []int32 = []int32{8, 9}
  intSlice = append(intSlice, intSlice2...)
  fmt.Println(intSlice)

  var intSlice3 []int32 = make([]int32, 3, 8)
  fmt.Println(intSlice3)

  var myMap map[string]uint8 = make(map[string]uint8)
  fmt.Println(myMap)

  var myMap2 = map[string]uint8{
    "Adam":23, 
    "Sarah": 45,
  }
  fmt.Println(myMap2)
  fmt.Println(myMap2["Adam"])
  fmt.Println(myMap2["Jason"])

  var age, ok = myMap2["Jason"]
  if ok {
    fmt.Printf("The age is %v", age)
  } else {
    fmt.Println("Invalid Name")
  }

  delete(myMap2, "Adam")

  for name := range myMap2 {
    fmt.Printf("Name: %v \n", name)
  }

  for name, age := range myMap2 {
    fmt.Printf("Name: %v, Age: %v \n", name, age)
  }

  for i, v := range intArr {
    fmt.Printf("Index: %v, Value %v \n", i, v)
  }

  fmt.Println("Loop 1")
  var i int = 0
  for i < 10 { // similar to while loop
    fmt.Println(i)
    i = i + 1
  }

  fmt.Println("Loop 2")
  i = 0
  for { // while (true) loop
    if i < 10 {
      fmt.Println(i)
      i = i + 1
    } else {
      break
    }
  }

  fmt.Println("Loop 3")
  for i := 0; i < 10; i++ { // for loop
    fmt.Println(i)
  }
}
```

## String, Runes and Bytes
```go
package main

import (
	"fmt"
	"strings"
)

// About UTF-98: https://stackoverflow.com/questions/43230082/why-adding-the-two-bytes-of-utf-8-encoding-doesnt-give-the-code-point-of-the-ch

func main() {
  var myString = "résumé"
  var indexed = myString[1]
  fmt.Printf("%v, %T\n", indexed, indexed)

  for i, v := range myString {
    fmt.Println(i, v) // range will skip some things 
  }

  fmt.Printf("The length of 'myString' is %v\n", len(myString))
  
  var myString2 = []rune("résumé")
  var indexed2 = myString2[1]
  fmt.Printf("%v, %T\n", indexed2, indexed2)

  for i, v := range myString2 {
    fmt.Println(i, v) // range will skip some things 
  }

  fmt.Printf("The length of 'myString2' is %v\n", len(myString2))
  
  var MyRune = 'a'
  fmt.Printf("myRune = %v\n", MyRune)

  var strSlices = []string{
    "s", "u", "b", "s", "c", "r", "i", "b", "e",
  }
  var catStr1 = ""
  for i := range strSlices {
    catStr1 += strSlices[i] // create a new string evertime
    // very inefficient
  }
  fmt.Printf("%v\n", catStr1)
  // String are imutable in go

  var strBuilder strings.Builder
  for i := range strSlices {
    strBuilder.WriteString(strSlices[i]) // efficient works like vector
  }
  var catStr2 = strBuilder.String()
  fmt.Printf("%v\n", catStr2)
}
```

## Structs and Interfaces
```go
package main

import "fmt"

type gasEngine struct {
  mpg uint8
  gallons uint8
  ownerInfo owner
}

type gasEngine2 struct {
  mpg uint8
  gallons uint8
  owner
}

type owner struct {
  name string
}

func main() {
  var myEngine gasEngine = gasEngine {
    25, 15, owner{"Alex"},
    // mpg: 25, gallons: 15, ownerInfo: owner{"Alex"},
  }
  myEngine.mpg = 20
  fmt.Println(myEngine.mpg, myEngine.gallons, myEngine.ownerInfo.name, myEngine.ownerInfo)
  
  var myEngine2 gasEngine2 = gasEngine2 {
    25, 15, owner{"Alex"},
  }
  fmt.Println(myEngine2.mpg, myEngine2.gallons, myEngine2.name, myEngine2.owner)
}
```


```go
package main

import "fmt"

type gasEngine struct {
  mpg uint8
  gallons uint8
}

func main() {
  var myEngine gasEngine = gasEngine{
    25, 15,
  }
  fmt.Println(myEngine)
  
  var myEngine2 = struct { // anonymous struct    
    mpg uint8
    gallons uint8
  } {25, 15} 
  fmt.Println(myEngine2)
}
```


```go
package main

import "fmt"

type gasEngine struct {
  mpg uint8
  gallons uint8
}

type electricEngine struct {
  mpkwh uint8
  kwh uint8
}

func (e gasEngine) milesLeft() uint8 {
  return e.gallons * e.mpg
}

func (e electricEngine) milesLeft() uint8 {
  return e.kwh * e.mpkwh
}

type engine interface {
  milesLeft() uint8
}

func canMakeIt(e engine, miles uint8) {
  if miles <= e.milesLeft() {
    fmt.Println("You can make it there!")
  } else {
    fmt.Println("Need to fuel up first!")
  }
}

func main() {
  var myEngine gasEngine = gasEngine{
    25, 15,
  }
  fmt.Println(myEngine)
  fmt.Printf("Total miles left in tank: %v\n", myEngine.milesLeft())
  
  var myEngine2 electricEngine = electricEngine{
    30, 20,
  }
  fmt.Println(myEngine2)
  fmt.Printf("Total miles left in tank: %v\n", myEngine2.milesLeft())
  
  canMakeIt(myEngine, 50)
  canMakeIt(myEngine2, 50)
}

```

## Pointers
```go
package main

import "fmt"

func main() {
  var p *int32 = new(int32) // default nil
  var i int32
  
  *p = 10
  
  fmt.Printf("The value p points to is: %v\n", *p)
  fmt.Printf("The value of i is: %v\n", i)

  p = &i
  *p = 1

  fmt.Printf("The value p points to is: %v\n", *p)

  fmt.Printf("The value of i is: %v\n", i)


  var slice = []int32 {1, 2, 3,}
  var sliceCopy = slice

  sliceCopy[2] = 4
  fmt.Println(slice)

  fmt.Println(sliceCopy)
}
```


```go
package main

import "fmt"

func main() {
  var thing1 = [5]float64 {1, 2, 3, 4, 5,}

  fmt.Printf("The memory location of thing1 array is: %p\n", &thing1)

  var result [5]float64 = square(&thing1)
  fmt.Printf("The result is: %v\n", result)
  fmt.Printf("The result is: %v\n", result)
}

func square(thing2 *[5]float64) [5]float64 {
  fmt.Printf("The memory location of thing2 array is: %p\n", thing2)
  for i := range thing2 {
    thing2[i] = thing2[i] * thing2[i]
  }
  return *thing2
}
```

## Gorutines
```go
package main

import (
  "fmt"
  "time"
  "sync"

)

/*
Goroutines
- launch multiple functions and execute them curcurrently
- concurrency != parallalism
- parallalism takes place with multi core cpu
*/

// var m = sync.Mutex {}
var m = sync.RWMutex {}
var wg = sync.WaitGroup {}
var dbData []string = []string {"id1", "id2", "id3", "id4", "id5", "id6"}
var results []string = []string {}

func main() {
  t0 := time.Now()

  for i := 0; i < len(dbData); i++ {
    wg.Add(1)
    go dbCall(i)
  }
  wg.Wait()
  fmt.Printf("Total execution time: %v\n", time.Since(t0))
  fmt.Printf("Total results are %v\n", results)
}

func dbCall(i int) {
  var delay float32 = 2000;
  time.Sleep(time.Duration(delay) * time.Microsecond)
  // fmt.Println("The result from the database id: ", dbData[i])
  
  // m.Lock() // placement of lock is really important
  // results = append(results, dbData[i])
  // m.Unlock()
  
  save(dbData[i])
  log()
  wg.Done()
}

func save(result string) {
  m.Lock()
  results = append(results, result)
  m.Unlock()
}

func log() {
  m.RLock() // many read lock possible
  fmt.Printf("The current results are: %v\n", results)
  m.RUnlock()
}
```

## Channels
```go
package main

import (
	"fmt"
	"time"
)

/*
Channels
- Goroutine to pass around information
- Hold data
- Thread Safe
- Listen for Data
*/

func main() {
  // var c = make(chan int) // waits for the main
  var c = make(chan int, 5) // doesn't wait for the main
  go process(c)
  // fmt.Println(<- c) // wait for the value to be set
  for i := range c {
    fmt.Println(i)
    time.Sleep(time.Second * 1)
  }

}

func process(c chan int) {
  defer close(c) // do this thing right before the function ends
  for i := 0; i < 5; i++ {
    c <- i
  }
  fmt.Println("Exiting process")
  // close(c)
}
```


```go
package main

import (
	"fmt"
  "math/rand"
	"time"
)

/*
Channels
- Goroutine to pass around information
- Hold data
- Thread Safe
- Listen for Data
*/

const MAX_CHICKEN_PRICE float32 = 5
const MAX_TOFU_PRICE float32 = 3

func main() {
  var chickenChannel = make(chan string)
  var tofuChannel = make(chan string)
  var websites []string = []string {
    "walmart.com", "costco.com", "wholefoods.com",
  }

  for i := range websites {
    go checkChickedPrices(websites[i], chickenChannel)
    go checkTofuPrices(websites[i], tofuChannel)
  }
  sendMessage(chickenChannel, tofuChannel)
}

func checkTofuPrices(website string, c chan string) {
  for {
    time.Sleep(time.Second * 1)
    var tofuPrice = rand.Float32() * 20
    if tofuPrice <= MAX_TOFU_PRICE {
      c <- website
      break
    }
  }
}

func checkChickedPrices(website string, chickenChannel chan string) {
  for {
    time.Sleep(time.Second * 1)
    var chickenPrice = rand.Float32() * 20
    if chickenPrice <= MAX_CHICKEN_PRICE {
      chickenChannel <- website
      break
    }
  }
}

func sendMessage(chickenChannel chan string, tofuChannel chan string) {
  select { // if statement for channels (doesn't neeed defer)
    case website := <- chickenChannel:
      fmt.Printf("Text Sent: Found deal on chicken at %v\n", website)
    case website := <- tofuChannel:
      fmt.Printf("Email Sent: Found deal on tofu at %v\n", website)
  }
}
```

## Generics
```go
package main

import "fmt"

func main() {
  var intSlice = []int{1, 2, 3}
  fmt.Println(sumSlice[int](intSlice))
  
  var float32Slice = []float32{1, 2, 3}
  fmt.Println(sumSlice[float32](float32Slice))
}

func sumSlice[T int | float32 | float64](slice []T) T {
  var sum T 
  for _, v := range slice {
    sum += v
  }
  return sum
}
```


```go
package main

import "fmt"

func main() {
  var intSlice = []int{1, 2, 3}
  fmt.Println(isEmpty(intSlice))
  
  var float32Slice = []float32{1, 2, 3}
  fmt.Println(isEmpty(float32Slice))
}

func isEmpty[T any](slice []T) bool {
  return len(slice) == 0
}
```

```go
package main

import (
	"fmt"
)

type gasEngine struct {
  gallons float32 
  mpg float32
}

type electricEngine struct {
  kwh float32
  mpkwh float32
}

type car [T gasEngine | electricEngine] struct {
  carMaker string
  carModel string 
  engine T
}

func main() {
  var garCar = car[gasEngine] {
    carMaker: "Honda",
    carModel: "Civic",
    engine: gasEngine {
      gallons: 12.4,
      mpg: 40,
    },
  }
  fmt.Println(garCar)

  var electricCar = car[electricEngine] {
    carMaker: "Tesla",
    carModel: "Model 3",
    engine: electricEngine {
      kwh: 57.5,
      mpkwh: 4.17,
    },
  }
  fmt.Println(electricCar)
}
```

