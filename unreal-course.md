# Unreal Course

These are my notes about the C++ Unreal Course on Udemy:
https://www.udemy.com/course/unrealcourse/

## Using vim for editor

I'm going to try to use vim for my IDE but if it goes wrong 

### Using vim-cpp

https://github.com/vim-jp/vim-cpp

## Compiling C++ on Linux

Pass the main file into `g++`

### Example

```
g++ main.cpp
```

**TODO**: We should probably create a `MakeFile` to simplify this process

#### Research

* https://www.gnu.org/software/make/manual/make.html
* https://courses.cs.washington.edu/courses/cse373/99au/unix/g++.html
* https://stackoverflow.com/questions/2481269/how-to-make-a-simple-c-makefile

## Triple Ex Game

### Design Doc

Hacking minigame

#### Why

* Feel like a cool hacker
* Be challenged by number puzzles

#### Mechanics

* 2 different challenges
** Guess must add up to given target
** Guess must be divisible by given number
* Starts easy but becomes harder
