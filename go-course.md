# Go Course

These are my notes about the Go: The Complete Developers Guide (Golang) course
on Udemy:

* https://www.udemy.com/course/go-the-complete-developers-guide

## Using vim for editor

Using vim to set up:

* install vim-go: https://github.com/fatih/vim-go
  * install the plugin (Vim8): 
    ```
    git clone https://github.com/fatih/vim-go.git ~/.vim/pack/plugins/start/vim-go
    ```
  * run the install: `:GoIinstallBinaries`

## Code Style

Go code style is strictly enforced and can be automatically cleaned up with:
```
go fmt
```

## Coursework Repo

# Project 1: Card Deck

## Compiling Go

```
go run main.go deck.go
```
runs both modules as they are both part of the `main` package

### Creating executeables

the `main` package will create an executeable. All other packages will not
create an executeable

so 

```
package apple

import (
    "fmt"
)

func main() {
    fmt.Println("Hello World")
}
```
will not create an executeable when compiled with `go build main.go`

## Creating types

```
type deck []string
```
creates a type called `deck` which will behave like `[]string`, much like a
subclass so we can use it like

```
deck{"One", "Two", "Three"}
```

### Adding functionality to custom types

create a function with a **receiver** (in this case `(d deck)`

```
func (d deck) print() {
    for i, card := range d {
        fmt.Println(i, card)
    }
}
```

* `d` is from type `deck` which is set up as `[]string`. By convention, this is
  a one or two letter variable from the type
* it loops through a range, exposing `i` and `card`
* `range d` allows iterating over a range (like `[]string`

Links

* https://gobyexample.com/range
* https://gobyexample.com/for

## using ranges in slices

we can use the following to set a range from within a slice

```
slicename[upToAndIncluding:FromNotIncluding]
```

so the following are true

```
mySlice := []string {"Apple", "Banana", "Orange", "Grape"}

mySlice[0:2]
// returns {"Apple", "Banana"}

mySlice[:2]
// returns {"Apple", "Banana"}

mySlice[2:4]
// returns {"Orange", "Grape"}

mySlice[2:]
// returns {"Orange", "Grape"}
```

Notes:
* the first number in the range is "up to and **including**"
* the first number can be omitted to infer from the start (0)
* the second number in the range is "from and **not including**"
* the second number can be omitted to infer to the end (4 in this case)

so a single number can be used on either side of the colon to select 2 subsets
whose total is the whole set

```
mySlice := []string {"Apple", "Banana", "Orange", "Grape"} 


fmt.Println(mySlice[2:])
// returns {"Orange", "Grape"}

fmt.Println(mySlice[:2])
// returns {"Apple", "Banana"}
```
