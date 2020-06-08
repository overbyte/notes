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
