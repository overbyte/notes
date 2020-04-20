# Unreal Course

These are my notes about the C++ Unreal Course on Udemy:
https://www.udemy.com/course/unrealcourse/

## Using vim for editor

I'm going to try to use vim for my IDE but if it goes wrong 

## Other notes

* [vim-cpp-setup.md](vim-cpp-setup.md)

## Code Style

[learncpp.com](https://www.learncpp.com/cpp-tutorial/whitespace-and-basic-formatting/)
doesn't have a preference for tabs vs spaces but does prefer 1TB (One True
Brace) style for brackets.

### Coursework Repo

https://github.com/overbyte/unrealcourse/


# Section 2 Triplex

[Coursework link](https://github.com/overbyte/unrealcourse/tree/master/section-2-triplex)

## Compiling C++ on Linux

Pass the main file into `g++`

### Example

```
g++ main.cpp -o applicationname
```

**TODO**: We should probably create a `MakeFile` to simplify this process

#### Research

* https://www.gnu.org/software/make/manual/make.html
* https://courses.cs.washington.edu/courses/cse373/99au/unix/g++.html
* https://stackoverflow.com/questions/2481269/how-to-make-a-simple-c-makefile

# Section 3 BullCowGame

[Coursework link](https://github.com/overbyte/unrealcourse/tree/master/section-3-bullcow)

## Notes

### const methods

const methods are methods which don't mutate member variables.

Example
```
void UBullCowGameCartridge::IsIsogram(FString Word) const
```

### Parameters vs Arguments

Parameters are given in a method declaration
Arguments are the values that are passed using the parameters

### Using References

When we use the following in our method declaration:

```
void UBullCowGameCartridge::MyMethod(FString Guess)
```
we are actually taking a copy of the Guess FString that is passed as an
argument. If we don't intend to mutate that variable, it is more efficient to
use a reference to the original variable. 

This is done with a & at the end of the type:
```
bool IsIsogram(const FString& Word) const;
```

It is preferable to make this a `const` because it would be a bad side effect to
mutate the original variable unless you want to use an out parameter

#### Using out parameters

To use an out parameter, we declare a variable outside the method, use a
non-const reference parameter and mutate the state of that variable from within
the method. 

Seems shady as balls - all side-effect.

Example:
```
int32 Bulls, Cows;
GetBullCows(Guess, Bulls, Cows);

void UBullCowCartridge::GetBullCows(const FString& Guess, int32& BullCount, int32& CowCount) 
{
    ...
```
