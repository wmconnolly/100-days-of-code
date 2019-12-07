# 100 Days Of Code - Log

### Day 0: October 2, 2019

**Today's Progress**: Today I've made the decision to launch into the often seen '100 days of code' challenge, with the goal of learning `Go`; a language that is relatively new to me. After choosing the book _"Go in Action"_ I've settled on the following approach to the 100 days challenge: Read the book, explore the corresponding code (locally), and document my takeaways each day. If I end up with self-written code from a particular day, I'll post that too; though that may not be a frequent outcome. Otherwise, today I've setup vim-go, read up to page 94 (that includes readings before starting the challenge), and put this repository in motion!

**Thoughts:** What's impressing me most from Go so far is what _it lacks_, or at least what it contstrains (i.e. formatting). From my perspective this is awesome, because as a new learner I feel my ramp-up time will be relatively quicker compared to that of a looser language, where there's a 'yes, do this; but...' to seemingly every aspect of the language. The only 'batteries included' aspect I see in Go, so far, is in its concurrency considerations - I am very excited by this, and feel the work done by the authors / core team will open up a sphere of programming that would otherwise be too prohibitive for my (current) non-professional relationship to computer science. A language which effectively handles events which may or may not depend on eachother, or to happen simultaneously is just _really really_ cool; no wonder Go has emerged as foundational tool for IT infrastructure. For day 1, I'll probably take a look at Go's type system, and reproduce some notes on that.

---

### Day 1: October 3, 2019

**Today's Progress**: A valuable lesson into Go's environment variables and its packaging approaches. Tried actually running _Go in Action_'s chapter 2 code, an RSS feed crawler; returning news stories which match a parameter in `main.go`. Cloning the repository to my home directory proved just fine, I've been _looking_ at the code on my machine in-step with reading the book. Though changing into the filepath for chatper2's code, and running `go run main.go` supplied the following error:

```bash
main.go:7:2: cannot find package "github.com/goinaction/code/chapter2/sample/matchers" in any of:
	/usr/local/go/src/github.com/goinaction/code/chapter2/sample/matchers (from $GOROOT)
	/Users/kylcon/go/src/github.com/goinaction/code/chapter2/sample/matchers (from $GOPATH)
main.go:8:2: cannot find package "github.com/goinaction/code/chapter2/sample/search" in any of:
	/usr/local/go/src/github.com/goinaction/code/chapter2/sample/search (from $GOROOT)
	/Users/kylcon/go/src/github.com/goinaction/code/chapter2/sample/search (from $GOPATH)
```

...uh, why isn't this working? Right!? I'm able to whip up a 'hello world' `main.go` _pretty much anywhere on my local machine_ **and it runs**.

It runs because my installation of Go successfully updated my `$PATH`, and I'm using the conventional `$HOME/go/` directory structure, and I'm not importing packages outside the standard library. What I didn't understand in placing the book's repository in `~/` was that imports made using `github.com/{...}` have specific meaning.

My `go run main.go` registered just fine, but trying to run main, and every other file in each package, was trying to import against a filepath which didn't relatively exist. After _not really reading the error message given to me_, I moved the code around a bunch, Googled it, realized my error, then placed it in the proper place.
**Check this documentation out:** [Remote import paths](https://golang.org/cmd/go/#hdr-Remote_import_paths)

_Voilá_. It was really cool to actually run chapter2's program, and _wow was it FAST_. Toying with the searched parameter, turns out NASA has produced a computer model of a black hole in 3D; as reported by NPR: [NASA's New Black Hole Model
](https://www.npr.org/2019/10/03/766706899/nasas-new-black-hole-model)

**Thoughts:** _Errors aren't evil_. Use them when you get them, Go's structure will be an adjustment; though I believe it's actually much clearer than having a cocktail of global/local dependecies. Go certainly does allow for globally available packages, however, I think to have them is just a bit more explicit of a process; and if you're coming to Go from where I am - explicit is better than implicit ;)

---

## Day 2: October 4, 2019

**Today's Progress:**
Finished walking through _Go in Action_'s chapter 2 code. There is a disclaimer in the beginning of the chapter that it's ok _not to_ fully understand the code the first, second, maybe even third time through. Good disclaimer! The example is a well organised bit of Go code, I'm sure; though it's _much too_ complex for me to feel like I'm building up a base with the language -- too much 'plate spinning' upfront. Having said that, the chapter **certainly** imparts some great insight about the language. A few points on that:

- `Go` passes all variables by **value**, not reference. So, pointer variables allow direct modification of variables out of function scope -- this is useful in sharing variables between functions, even concurrent `goroutines`
- Pulling out a value from a map (like a Python dictionary, or JS object), you have the option to assign a second, boolean variable from the return of the `'map'[key]` lookup.
  ie
  `go value, found := someMapObject[key]`
  `found` equals true when there's an entry for the lookup, false otherwise. This is cool!

- Uppercase means it's exported! Uppercase named things can be accessed from outside the code file which defines it. lowercased items cannot be _directly_ accessed from outside. This will be important for me to keep in mind.

**Thoughts:** _Go in Action_ is without a doubt a great book, however; I'll need to replace it with a resource that presents Go in more of a compartmentalised way so that I can really soak in the basics. _Go in Action_ should help to drive home the language in a wholistic view, and I'll be sure to spend five minutes with it at the end of each day. _Go by Example_ will be my primary resource for now.

---

## Day 3, October 5, 2019

**Today's Progress:** `variables, contstants, for loops`.

- `var` or `const` is required when a named value isn't initialized on declaration.
- `const` is acutally constant, no symbolism here :D
- `for` loops have a few different constructions, get one, and you can confidently infer the others
  - simultaneous arithmetic operation/assignment works `+=, *=, -=` will all act on your incrementing variable!
  - _`for` is the only loop available_

**Thoughts:** Given that `for` is the only loop in Go, I'm curious what the idiomatic pattern is to replicate a `while` loop... _what's the best-practice sential value?_ The way Go shakes off inheritance in favour for composition gives the language huge leverage. You can still _write_ code with a sort-of object orientation, but it's **functional**. With this kind of 'plug and play' approach, I'm not surprised to read frequently that folks applaud Go as a language for implementing microservices. So excited to ramp up in this language, and (hopefully) build useful things!

---

## Day 4, October 6, 2019

**Today's Progress:**

- Covered in _Go by Example_: `if / else / switch / array / slice` + you can declare / init a variable within a conditional check, and continue to use it in the _same conditional branch it was created within_
  - arrays are of fixed length and type + slices are arrays with dynamic length (ie still singularly typed) + both can be multi-dimensional, and use the `[:]` syntax to take _slices_
    around objects in `Go` + switch cases check for equality: either value or type, depending on how the case is presented. i.e `case 3:` checks that the `switch` specified var equals interger 3. `case bool:` check that the given var is a `boolean` type.
- The `package` _is_ the orientation around creating objects

**Thoughts:** Currently mulling over the thought that Python spoils developers with it's dynamic lists, and list comprehension syntax. Highly interested to see whether `Go` has an approach, or if I'll just have to get used to the array / slice structures; which would be a net-good thing. Really enjoying learning this language

## Day 5, October 7, 2019

**Today's Progress:** Relatively minimal today in terms of topics covered, but the syntax felt like it's actually starting to soak-in. Looked at the `map` associative data type, and the `range` iterator. Unless there's another iterator which will pop-up later, it looks as if `Go` has _one_ loop, and iterator keyword. Simple, nice.
A few observations from today:

- to initialize slices and maps, we primarily use the `make` keyword. Haven't seen Arrays made with make, and contain its defined length inside `[]`
- the `:=` syntax is _only used_ when initialising a variable. **Should** be, and is, obvious; but really started to feel the truth of it in my fingers for first time
- `range` returns the index of the iterable first, values second. If index isn't needed, use the `_` ignore var. With maps, we easily have choice of key/value or just key
- `map` has typed keys AND values. Ridgid typing, but I can picture the saved confusion of trying to pin-point what 'xyz' is at any given point -- we'll know, becuase we've typed it that way.

  **Thoughts:** It's super easy to become distracted with tooling, but with _just_ enough discipline, the attention paid to refining it is high-value... In Vim, I can now run my little sandbox `main.go` via a simple `<leader>r` -- rock on.

---

## Day 6, October 8, 2019

**Today's Progress:**

- Functions

  - Go does not implicitly return, we _must_ use a `return` statement
  - Return value(s) typed just before launching into a `{...}` code block
  - The blank identifier `_` is used to move past irrelevant return values, when a function returns more than one value
  - Can accept several different types of parameters, but can only accept one type of varying number of args, declared as the last parameter in the function's signature.
    ```go
    func exName(arg1 int, arg2 string, variadic ...int) {...}
    ```
  - Closures have access to variables from the scope above the anonymous function's declaration, but I'm going to have to step through this again tomorrow!

  **Thoughts:** Family circumstances will make the challenge more difficult to fulfil, but I'm prepared to cut through the challenge. First of three challenging days in the books!

---

## Day 7, October 9, 2019

**Today's Progress:** Closures click much better now.

```go
func theClosure() func(ifParam type) type {
  outerStateVar := value
  return func(ifParam type) type {
    `do work`
    return outerStateVar
  }
}
```

**Thoughts:** What was confusing me yesterday, and what I still don't _fully_ understand why today, is the named function signature; specifically why we can't do something like:

```go
func theClosure() func {
  return func(param type) type {
    work...
    }
}
```

I've got questions about the anonymous function being in-place of the named function's return type. **Maybe** that's the point? Perhaps the return type of a function which returns a function is the fully typed signature of that inner (anon) function?

... While I'm not the _best_ at math, I often wonder if I would have enjoyed a CS degree more than my one in commerce.

In any event, closures in Go are cool.

---

## Day 8, October 10, 2019

**Today's Progress:**

- Recursion
  - If condition on the argument isn't met, it returns a call to itself with the argument modified in some way
- Pointers

  - Thinking about this like deep v shallow [e.g. copying]

  ```go
  a := 1
  b := a // b now has the [face]value of 1
  a = 2
  fmt.Println(b) // outputs 1 for reason above
  ```

  not using a pointer literally hard codes the value of the existing varialbe (`a` in this case) at time of assignment

  ```go
  a := "point to this"
  b := &a // b now equals the address in memory of a, or 'points' to the memory address
  fmt.Println(b) // outputs memory addr
  fmt.Println(*b) // outputs a's value; "point to this"
  ```

- Structs

  - Look like a map; key/type (...then value) pairs under the umbrella of a custom type

  ```go
  type Custom struct {
    prop1: string
    prop2: int
    isAwesome: bool
  }
  ```

  Need to init structs with explicit values for each field, or key.

  **Thoughts:** Need to revist structs tomorrow - tired. Having said that, tonight is day three of three days this week which were more of a challenge to make time/space to focus on #100Days; so I'm pleased! Loving Go... I thought I didn't like strongly typed languages :)

---

## Day 9, October 11, 2019

**Today's Progress:**

- Correction on initing a `struct`

  - It's totally possible to initialize a `struct` with partial values.

  ```go
  type Custom struct {
    field1 string
    field2 int
    field3 bool
  }

  example := Custom{field1: "test"} // the other struct fields are initialized using their respective zero-value
  // update other properties of the struct via the `dot` operator
  example.field2 = 10
  example.field3 = true

  // Go by Example states idiomatic inits of structs are as follows:
  type yourStruct struct {
    prop string
    field int
    etc etc
  }

  func createyourStruct(param type) *yourStruct {
    creation := yourStruct{prop: param}
    return &creation
  }

  // Return type is a pointer to the definition of the struct, return statement returns the created struct's address in memory
  ```

- Methods, act on structs and either:
  - return using data from struct with changing the underlying instance
    - or
  - mutate the struct, and return

**Thoughts:** tomorrow is Saturday, and I will do most of the study / exploration early in the day; today I came back, looked at structs and realised I had better re-assess them before moving onto methods and interfaces. Fortunately, I'm well setup for methods, as the idiomatic way to init them is via a constructor _method_!

**But bottom line is: running through several topics at the end of a work day leaves memory gaps, and therefore a need to reiterate topics.**

_Hasten slowly_, as the motto goes :)

---

## Day 10, October 12, 2019

**Today's Progress:**

- To write `methods` ask yourself:

  - Make calculation w/ existing `struct` data, or
  - Change the underlying data of the `struct` you make a method call from?

  ```go
  func (varName structName) actualFuncName(ifParams type) returnType {
    // are you changing the struct's underlying values? You need to `*` point to the struct in the function signature's header if so.
  }
  ```

- Interfaces

  - An `interface` is a data type to store a set of `method` signatures
    - It's about structs similiar in nature, sharing common methods... i.e. not all fish are the same, but all fish swim
  - If a `struct` is a named collection of primitive data types, an `interface` is a named collection of methods (which are capable of acting on structs similar in nature)

- `goroutines`
  - A _lightweight_ thread of execution, a thread is a piece of computation within a process, multiple can be run at the same time; said to be _concurrent_. As a hobbyist programmer, I'm sure my mental model, and technical understanding of concurrent computation will mature. As it does, I'm reminded of people who can spin many plates...
    - [Spinning plates](https://giphy.com/gifs/lVzwf1CLZt9As/html5)...
      where the stick person is the process, dowels are the threads, and plates equal the code to compute

**Thoughts:** While I belive I understand the role of interfaces, I'm not sure I entirely appreciate their use. If the methods generalised by an `interface` need to be declared for each `struct` individually... why not just call the `method` off the `struct`? This though is compounded by an idiomatic approach seen in _single method interfaces_... My mind needs to grow and evolve with this one!

---

## Day 11, October 13, 2019

**Today's Progress:** Relatively slow day, not _much_ that's new covered. But reproduced the execution chops of a goroutine by achieving a kind of recursion-in-a-closure like function; which I'll walk through now!

```go
package main
import (
  "fmt"
  "time"
)

func increment(i *int) int {
  n := *i + 1
  *i := n
  return increment(i)
}

func main() {
  count := 0
  go increment(&count)
  time.Sleep(time.Second)
  fmt.Print(count)
}
```

So while this short `main` launches a go routine, I believe it's actually, non-chalantly, about pointers / pass-by-reference deep down.

For `count` to increment on each recursive call of `increment`, it has to be the _same_ `count` used ... so `increment` needs to receive a variable pointing to memory, type `int`. We're incrementing by 1; the return type is also `int`.

In the function body, `n` handles adding one to our current `count` value, then we assign the value of `n` back into `i` (`count`... by its memory _reference_).

Our return value is the recursion, passing `i` without an asterisk. In the function body, we're referring to `*i` because we need to deal with the `int` value for `i` at the time. In the return, we're passing `i` back into our function _as a type identified as a pointer in the function signature_. I'm enjoying thinking about the "\*" as a dot, or a 'point'; denoting our code **points** to the **value** of the namespace we're referring to.

When we launch the goroutine, we pass `increment` the `count` variable above, but prefixed with an ampersand... `&` denotes the _memory address_ of that variable, and our function is expecting an arugment which can _point_ to a value... `&count` allows the function to execute passing by reference.

The output of the small scrip above, on my machine (a 2018 Macbook Air), gives `count` a final value of `8388579`

...8,388,579 times, `count` was incremented by 1, _in one second_. This language is WILD

**Thoughts:**
Throughout the learning process, I think it's important to always take pause and ask the question _"how can I use what I've learned so far to solve a problem I currently have?"_.

Learning concepts is one thing, converting them into concrete code is a whole different ball game.

---

## Day 12, October 14, 2019

**Today's Progress:** Today is a bit of a mulligan; today was a national holiday in my country, though I worked, helped prepare the family meal for the holiday, then had a four-hour journey to help family with car trouble on their way back to home. So I came to today _late_ and **tired**. I have hopped onto "P4L", a new online course in Computational Thinking / Programming offered by Carnegie Mellon. Today's lecture is about the Ancient Greeks, and the origin of computational thinking. I joined 100+ minutes after its start. I will catch up tomorrow. This is all the brain power I have for today :)

**Thoughts:** The prepared make easy work of foreseen challenges, the stalwart makes challenges unforeseen seem planned. The hardest parts of the challenge is to stick with it when you've got to totally improvise in your day. Despite a lackluster day of programming / expirementing, I hope this serves as a small example of being stalwart in my approach to 100 Days Of Code

---

## Day 13, October 15, 2019

**Today's Progress:** Caught up on the first lecture of P4L, quite glad I did; the course approach is interesting. The language of instruction _will be Go_ but there's an early emphasis on thinking computationally a language agnostic way. There's realy value to that, doing so leads you to a deeper truth of what programming **is**, a language always just being a specific implementation of that. Pseudocode is a universally interpreted language, compiled by the programmer ;). Pseudocode is an opportunity to excercise 'deep work' on the problem at hand.

**Thoughts:** Go is an awesome, modern language I am so excited to pickup; but reasoning and crafting logic is timeless.

---

## Day 14, October 16, 2019

**Today's Progress:** Watched a P4L-related video on debugging. A few debugging items to internalise:

- Read the error in-full
  - what context does it add?
- Frame the problem
  - where's the edge case?
- Assess code bottom-up
- Take breaks every 20 minutes
  - do not sacrifice sleep!

`chan` - explored channels to see how they fit with goroutines.

- `chan` is a typed data structure, I'm thinking about them as _slices dedicated for concurrency_
  - `yourChan := make(chan string)`
- data follows the `<-` flow; values moving from right into the left
  - `yourChan <- "Some text here"`
  - `someValue <- yourChan`
    - plucking out a value held in a channel

**Thoughts:** being able to iterate through a `chan` with `range` is still unclear to me. I will be coming back to this tomorrow, I feel I've got an intermediary step wrong as I seem to produce a "deadlock!" error.

---

## Day 15, October 17, 2019

**Today's Progress:** Now I better understand why yesterday's ranging over a channel produced this _goroutines asleep, deadlock!_ error. Making a `chan` "opens" the channel for communication; recieving data from concurrent functions. A channel is open until explicityly **closed**. So, the `range` operator over a `chan` which has yet to close is an infinite loop... hence the error telling me _"goroutines are asleep"_, ie no functions are running, therefore the program has reached a _"deadlock!"_. Functioning `main.go` example below:

```go
package main

import "fmt"

func addtochan(i int, c chan int) {
    for i := i; i <= 10; i++ {
        c <- i
    }
    close(c) // channel needs to be closed!
}

func main() {
    testChan := make(chan int)
    go addtochan(0, testChan)
    for num := range testChan {
        fmt.Printf("%v ", num)
    }
}
// output: 0 1 2 3 4 5 6 7 8 9 10
```

**Thoughts:**

---

## Day 16, October 18, 2019

**Today's Progress:** Today's progress was made a few steps back from Go's syntax / language features, or dynamics; more about underlying mathematics in programming (via certain algorithms specifically). This is a result of taking part in Carnegie Mellon's new, freely offered "Programming For Lovers" course (featuring Go). The nature of today's progress is _actually exactly why I decided to make this part of my 100 Days challenge_. So, specifics; most of my time was spent re-visiting permutations and combinations.

In short: for example, there are 5 items available for selection say programming languages to learn; Python, Javascript, Ruby, PHP, Go. Say you've decided to learn _two_ of those languages.

The **combinations** of those two languages are unique picks consiting of two languages. ie:

    - Python
    - Go

The **permutations** of those two languages considers _in what order you'll learn those languages_ ie:

1. Python
2. Go

**or**

1. Go
2. Python

_etc..._

Combinations == unique _groups_
Permutations == unique _orders_

- of choice `n`

**Thoughts:** Tomorrow I will detail the math, and implement in `Go`

---

## Day 17, October 19, 2019

**Today's Progress:** Wrote Permutations and Combinations in Go, which is working up to limits `20` for Combination option size, `20` and `19` for Permutation option and selection size. Numbers larger than these overflow, I've yet to figure out how to perform the calculation without involving the `math/big` package...

```go
package main

import "fmt"

func Fact(n uint64) uint64 {
    curr := n
    for i := n; i > 1; i-- {
        curr = curr * (i - 1)
    }
    return curr
}

func Perm(n, k uint64) uint64 {
    nom := Fact(n)
    den := Fact((n - k))
    res := nom / den
    fmt.Print(res)

func Comb(n, k uint64) uint64 {
    nom := Fact(n)

    den := Fact(k) * Fact(n-k)
    res := nom / den
    fmt.Print(res)
    return res
}

func main() {
    Perm(20, 19)
}

// outputs 2432902008176640000 (!!)
```

**Thoughts:** While this _is_ driving me crazy, and I want to figure this out, I'm asking myself whether this is a problem **I will** encounter in my real-world programming; in the interest of time, I will move on for now :)

---

## Day 18, October 20, 2019

**Today's Progress:** Reviewed some String formatting materials, and the `time` package for timing program execution.

**Thoughts:** Starting to look for ways I can solve some of my own problems using Go; I feel that'll be the next step in truly learning the language.

---

## Day 19, October 21, 2019

**Today's Progress:** Go in Action - with more topics covered in Go by Example, and P4L; I continued to read further into chapter 3. Rather than execute the book's code examples readily available via GitHub, I decided to write through it, and reproduce functionality according to `func` names. Great exercise for sure!

**Thoughts:** A quick re-visit / explanation on the `*` and `&` syntax:

- `&` represents the memory address of a variable
  - kinda like saying, _"oh `myVal` is on Heap & 0xc00009a000"_
- `*` is an asteriks, a dot; a _point_
  - it denotes **pointing** to an actual data type _value_

---

## Day 20, October 22, 2019

**Today's Progress:** Since starting my journey with Go, I've been printing to std out exclusively with the `fmt` functions. Today, I've realised there's a `print()` and `println()` baked right in... This is lots welcome - perfect for my stage of poking around / experimenting with the language. Saving a few keystrokes on something oft typed _is a delight_.

Chipped away at a little code challenge, experience the following:

- if you `range` through a `string`, the iterated value from the string is an `int` type, not a `string`.
  - Given `"abc"` - the value index `2` != `"c"`, but rather `99` - the integer value of a `string` equals that of a `rune`
- `fmt.Sprintf` returns (not actually prints) a `string` value perfect for splicing data types into a string

  **Thoughts:** While it was a slow process, it's a great exercise to solve problems like this, and concretely implement the readings / learnings from all other sources

---

## Day 21, October 23, 2019

**Today's Progress:** Worked through four more code katas today. Really enjoyed it, also caught up with Monday's P4L 1:50 lecture focusing on algorithms inherent to DNA pattern finding / counting.

- an interesting idiom came from it; leveraging the `map` datatype and a boolean check whether the key (pattern built from subindexing a string) exists

**Thoughts:** The map idiom reminds me of a quote of Rob Pike's I've seen recently:

> Data dominates. If you've chosen the right data structures and organized things well, the algorithms will almost always be self-evident. Data structures, not algorithms, are central to programming.
>
> [ Rob Pike's 5 Rules of Programming
> ](https://users.ece.utexas.edu/~adnan/pike.html)

Can't wait to embed this approach to programming, and hopefully increase my ability to leverage the programming language as it's built

---

## Day 22, October 24, 2019

**Today's Progress:** Watched and participated in the first 65 minutes of today's P4L lecture. Covering some data types and algorithm approaches.
**Thoughts:** Pseudocode is **king**

---

## Day 23, October 25, 2019

**Today's Progress:** Go in Action: finished chapter 3, began chapter 4 which covers the collection data types; `arrays`, `slices`, and `maps`. The book declares "arrays form the base data structure for both slices and maps", and "once you learn how these data structures work, programming in Go will become fun, fast, and flexible."

Go is certainly already fast, and fun, I don't doubt it's flexible; but I will dedicate the weekend to covering chapter 4 and really having these basics sink in. The basics are always _most_ important.

`go doc` automatically documents our code with these two conventions:

- Comments directly ontop of the declaration
- Use full sentences, first calling out the namespace of the item being _documented_

  - ie

    ```go
    // MyFunc takes a ... returns x.
    func MyFunc(x type)....
    ```

**Thoughts:** Practice 1 punch 10,000 times, rather than 10,000 punches once

---

## Day 24, October 26, 2019

**Today's Progress:** Go in Action: read through arrays, and most of slices in Chapter 4.

- If needing to pass a large array into a function, it's best to pass as a pointer, huge memory savings this way
- Slices, perhaps unsurprisingly, are built ontop of arrays
  - Sub-sliced slices share the same underlying array
  - Slices have a length, but also a capacity for a total number of elements the slice can hold
    - When a slice is appended to without existing capacity, `Go` re-assigns values in an underlying array, and doubles the capacity of the slice if capacity < 1000; 1.25x for slice capacities > 1000.

**Thoughts:** Will finish Ch 4 tomorrow, but want to read a bit less and code a bit more!

---

## Day 25, October 27, 2019

**Today's Progress:** Finished Chapter 4. The idiomatic way to create maps is a literal
`someMap := map[keyType]valueType{...}`
inside the curly brackets can have specific values, or left empty to create an empty map. Syntax example for a literal with specific values:
`yourMap := map[int]string{1: "first key/value", 2: "a second key/value"}`

**Thoughts:** The `slice` and `map` types are abstractions from an underlying `array` which holds the data. Because of this, it's cheap to pass slices or maps to functions (the data is _not_ copied for the func scope). Conversly, it's expensive to pass an `array` because the underlying data is copied; best practice is to pass a pointer variable to a function.

---

## Day 26, October 28, 2019

**Today's Progress:** P4L lectures, coding challenges, and review of Ch 4's highlights

**Thoughts:** Do more challenges tomorrow!

---

## Day 27, October 29, 2019

**Today's Progress:** Go in Action - began Ch 5, Go's type system. The idiomatic way to initialise a variable to its zero-value is with the `var` keyword. Also, it's possible to create custom types which effectively aliases other types. Both items in one ie:

```go
type age int
// ....
var myage age
myage = 28
```

Several coding challenges tonight, it has been the best tweak I've made to my 100 Days approach. More tomorrow!

**Thoughts:** Peak productivity is an equillibrium between activity and efficiency; in the context of learning Go, I find this to mean I'm getting the most out of reading (best practices, available tools, etc) and then solving/typing some code katas.

---

## Day 28, October 30, 2019

**Today's Progress:** Spent little time reading today, mostly worked on katas (completed three).

**Thoughts:** The shift made by working on katas is that it puts your mind into a _"how do I solve this problem"_ mode. It isolates a hurdle overwhich we can jump with code. I'm really starting to look for **business-value** items in my day-job I could write a `Go` script for... We shall see ^.^

---

## Day 29, October 31, 2019

**Today's Progress:** Go in Action: good reading on value / pointer receivers today. And learned Go will actually produce the proper receiver based on the specific kind of type which is calling the `method`.

Solved katas again, actually planned the required math with pen and paper before typing any code! This is usually a difficult practice for me; I like to be fingers on-keyboard, even though that can drag-out effective problem solving.

**Thoughts:** Still looking for something practical to implement Go in my day job...

---

## Day 30, November 1, 2019

**Today's Progress:** Primarily reading today. Go in Action: Chapter 5; _the nature of types_. `primitive` and `reference` types are generally passed to methods via `value` receivers _not_ via `pointer receivers`. Considering the buildingblocks of a `struct` can warrant `pointer` receivers... More to follow

**Thoughts:**

---

## Day 31, November 2, 2019

**Today's Progress:** Go in Action, Ch 5, through to Method Sets.
Choosing a receiver type depends on the complexity of the `struct` being passed in.

- primitive type stucts => value receiever
- nonprimitives => pointer reciever

An `interface` is a type which declares behaviour... Like a way to generalise functionality. Interfaces are data structures with two fields:

1. a pointer to an `iTable` (contains type info of the stored value)
2. a pointer to the actual stored value

Spent time experimenting with the `net` and `net/http` packages.

**Thoughts:** While generally familiar with HTTP, and knowing that Go's implementation is highly effective, it still felt like a lot of code to think through. I suppose this is inherent to the learning process; a cycle between confusion and comprehension. Will come back to this tomorrow.

---

## Day 32, November 3, 2019

**Today's Progress:** Lots of reading on `net/http`. Had a few examples running, though a full understanding of how and _why_ it works eludes me. Code kata, which was essentially about leveraging the `strings` package.

**Thoughts:** The 100 Days challenge is fantastic, though a true and genuine; professional-grade understanding will take _much_ longer. Can build this with the habits built by doing the 100 Days challenge

---

## Day 33, November 4, 2019

**Today's Progress:** Just katas today. After much reading over the weekend, I thought it best to only work on concrete challenges today. Here's how I solved finding the largest sum of a sub-set in an `int` slice:

```go
func MaximumSubarraySum(numbers []int) int {
    var result int
    for i := range numbers {
        for j := range numbers[i:] {
            var check int
            for _, num := range numbers[j:] {
                check += num
                if check > result {
                    result = check
                }
            }

        }
    }
    return result
}
```

The challenge exists in conceeding that negative, or low-value ints may be between high-value ints of sub-slice which makeup for the lower values. Always checking the sum, and re-assignig to `result` if greater than that of the _last_ check captures the highest sum regardless if `check` begin to diminish; seeing as it _will not_ be less than `result`.

**Thoughts:** Had fun today!

---

## Day 34, November 5, 2019

**Today's Progress:** Code katas only today, currently stuck on a 'Diophante' equation. I've got a working solution, though it needs to be refactored so it executes in a reasonable amount of time.

**Thoughts:** Will continue reading tomorrow

---

## Day 35, November 6, 2019

**Today's Progress:** Read Ch. 5, looking at Interfaces again, also watched watched a tech talk on idiomatic Go practices. Posting this progress the day after, because I fell asleep reading

**Thoughts:**

---

## Day 36, November 7, 2019

**Today's Progress:** Continued Ch. 5, Diophantine kata; still stuck...

**Thoughts:**

---

## Day 37, November 8, 2019

**Today's Progress:** Katas only today. Made progress with Diophantine, though I still have yet to produce a solution which _doesn't_ time out.

```go
import "math"

func Solequa(n int) [][]int {
    calc := [][]int{}
    if n < 0 {
        return calc
    }
    sqrn := int(math.Sqrt(float64(n)))
    for x := n; x > sqrn; x-- {
        y := int(math.Sqrt(float64((x*x - n) / 4)))
        if ((x - 2*y) * (x + 2*y)) == n {
            calc = append(calc, []int{x, y})
        }
    }
    return calc
}
```

At least now I'm only using one loop, but my math is weak; so I'm still trying to pickout the blindspot here. I've saved this kata for now, and moved on to others as so I don't dwell too long on this at one time.

**Thoughts:**

---

## Day 38, November 9, 2019

j
**Today's Progress:** Katas only today.

**Thoughts:**

---

## Day 39, November 10, 2019

**Today's Progress:** Katas only today, too.

**Thoughts:** Katas have been great, though it's certainly time to pick back up the books, etc. and continue to expand on Go as a language.

---

## Day 40, November 11, 2019

**Today's Progress:** Go in Action: embedded types, and some katas

**Thoughts:**

---

## Day 41, November 12, 2019

**Today's Progress:** Katas, light reading

**Thoughts:**

---

## Day 42, November 13, 2019

**Today's Progress:** Began work on developing a script to update a clou-hosted spreadsheet based on updates I receive in a separate Excel. Have my Go http client authorized, and accepting the JSON payload - I have the option of receiving it as a CSV; debating which encoding I should opt for. Will explore this tomorrow!

**Thoughts:** Excited to find a way of using Go in my day job

---

## Day 43, November 14, 2019

**Today's Progress:** Decided to use JSON for this project, as making a PUT request with the updates may force the loss of metadta which I use in other reporting.

The Go's way of handling JSON data is interesting; you basically replicate the JSON key/values into your own custom types, and 'decode' into an instance of the type. Still playing around with getting this right, will include snippets once I've got a solid grasp of my types.

**Thoughts:** Feeling the tax of Go with this learning curve, as compared to doing the same thing in Python. Having said that, Go still feels quite high-level considering it can be fittingly used for lower-level purposes.

---

## Day 44, November 15, 2019

**Today's Progress:** Made progress in parsing the JSON data. Yesterday, I began to wrestle with how to reliably access data, from a list, re-using the same `key`, but with differing data types depended on the column. Unmarshalling into a strictly typed `struct` was intermittently successful as a result.

The answer lies in two facets:

1. `[]interface{}` is the Go type for JSON arrays
2. `map[string]interface{}` is the Go type for JSON objects

So the JSON from the API looks like:

- sheet object
  - rows array of row objects
    - cells array of cell objects
      - key/values; ie `"displayValue": {bool || string || float64 || nil}`

Now being able to store the array of cell objects in a slice of interfaces, I can convert each cell JSON obj to a Go map; and process accordingly.

**Thoughts:** Still early days here, but great learning.

---

## Day 45, November 16, 2019

**Today's Progress:** With having the issue of dealing with varying types of a `cell.value` solved, I spent my time thinking about how I'll pair the process of reading-in the necessary changes, finding the existing, corresponding row/cells, and posting changes.

The API is kind of silly, in that there's a `cell.columnId` and `.value / .displayValue` but _no `cell.columnName`_; to act on the right cell in Go's `map[string]interface{}` representation, I'll have to pluck out the corresponding column IDs into standalone variables and cross-check with the current cell's `.columnId`

i.e.

```go
type payload struct {
    Name    string
    Id      int
    Columns []cols
    Rows    []rows
}

var contractcol int
var statuscol int
var datecol int
for _, col := range ts.Columns {
    switch col.Name {
    case "contract number":
        contractcol = col.Id
    case "status":
        statuscol = col.Id
    case "date paid":
        datecol = col.Id
    }
  }

// if cell["columnId"] == contraclcol {do work}
```

**Thoughts:** Unless I'm missing something here, I the API seems a bit wonky? I wonder what the design choices were, and why.

---

## Day 46, November 17, 2019

**Today's Progress:** Reading in my CSV data of changes needed to be made, and wrote a small helper function to decompose each `record` into a struct. But because each cell needs a `type assertion` into its respective map, I only have one cell available to me at a time -- to act on the right rows of data, I need to cross reference multiple cell values against the given csv record. So, I could either do multiple `if` checks, then destructure the _next_ cell using the loop's index - or I could use a `bool` for each requirement, and only alter the targeted cells if all prove true. In this case, I'll ultimately be looping through the JSON array of `cell` objects twice (which doesn't feel _proper_). We'll see!

**Thoughts:** Still curious over this APIs design choices ^.^

---

## Day 47, November, 18

**Today's Progress:** Relatively light reading today, heavy lifting at my job today; little mental energy left by the end. Small downside to remote work in the easy illusion of _always being at work_.

**Thoughts:** `brainpower := interface{}`

---

## Day 48, November 19, 2019

**Today's Progress:** Wrote an initial function to return `true` or `false` on whether a row of cells is _relevant_ to the current 'update' record read-in from my CSV.

The challenge now for me to take on is to smooth over the representation of any given datapoint after it's been converted.

E.g: a CSV record is read into a slice of strings, regardless of _what_ the data is meant to be. Contrast to the generalisation of numbers in a JSON object to be represented as `float64` in Go. Need to make sure I'm comparing apples to apples!

**Thoughts:**

---

## Day 49, November 20, 2019

**Today's Progress:** Matching CSV rows to corresponding JSON objects from the cloud-based spreadsheet. Each `cell` has a `"displayValue"` field, which is always a string. a CSV `record` is always a string. So the comparison checks works accurately and cleanly in my code. Currently working out the inner, core logic of the program; and will then need to properly `PUT` the JSON to the sheet. Then this little project is effectively finished!

**Thoughts:**

---

## Day 50, November 21, 2019

**Today's Progress:** Changes from the CSV record are being made to the underlying JSON cell. Marshalling the Go representation, and handing off to the http client to `PUT` back into the cloud-spreadsheet. **Awesome**. It's working, after a few http 400 responses, I discovered a cell's values (which I do not need to check/change) aren't copying through to JSON - hard-coded data to check whether the PUT request works thereafter; it is!

So tomorrow I'll investigate this further, and make sure I don't have to be hack-y with the program. Otherwise this is a good-to-go program, with a month's worth of changes data incoming.

**Thoughts:**

---

## Day 51, November 22, 2019

**Today's Progress:** Reading today, some bits on the `os` package.

**Thoughts:**

---

## Day 52, November 23, 2019

**Today's Progress:** Began cleaning up my spreadsheet program, setting the filename dynamically by reading all files in the directory. Also watched some videos coming out of KubeCon19, did some industry reading, and setup VIM with code snippets - I think I'm ok now to _not_ keep typing `fmt.Printf(...)` char by char :). Or `if err != nil {...}`...

**Thoughts:** Little things make the difference, probably should have invested the time to optomise VIM a bit sooner!

---

## Day 53, November 24, 2019

**Today's Progress:** Started reading about `k3s` and serverless approaches, and I want to get into the Kubernetes realm; Docker and Kubernetes' being built in Go was a major factor in my deciding to learn the language - I see (from a distance) the impact both technologies are having in the enterprise applications / data center spaces.

**Thoughts:** Why doesn't my Mac have `systemd`?

---

## Day 54, November 25, 2019

**Today's Progress:** Finished (for now) refactoring my spreadsheet program. More time spent on k3s, learning how it's different than k8s; I feel silly for trying to install either directly on my Mac - Kubernetes is about orchestrating _Linux containers_ after all. OSS, Linux, _duhh_.

**Thoughts:** Raspberry Pi it is!

---

## Day 55, November 26, 2019

**Today's Progress:** Started reading _"Kubernetes: Up and Running"_ via a PDF freely given away by Microsoft Azure. Generally lose patience reading PDFs; will likely buy a physical copy, but this is incredibly helpful to kick-start my `k8s` journey. Also spent time scoping out a new work-related project I can use Go for: parsing PDF documents to produce tabular data which is used for other tracking purposes.

**Thoughts:**

---

## Day 56, November 27, 2019

**Today's Progress:** Kubernetes reading and video watching today, ordered a RPi 4, so will soon be setting up my 'home-lab'. Learned / realised today Pods can mount fibre channel volumes.

**Thoughts:** Wonder how often the containerisation and SAN worlds conjoin...

---

## Day 57, November 28, 2019

**Today's Progress:** Installed `kubectl` and `minikube` on my machine, hoping to explore Kubernetes hands-on as much as possible before my Raspberry Pi arrives next week. Having trouble with `minikube start` and my VirtualBox installation; using the embedded KataKoda on kubernetes.io

**Thoughts:**

---

## Day 58, November 29, 2019

**Today's Progress:** More _Kubernetes: Up and Running_ reading today; still reading through the high-level descriptions, and components. What I most have internalised is that Kubernetes implements an immutable 'snap shot' of an application + infrastructure. Immutability is achieved via containers / container images. Virtual Box isn't playing nice on my machine; I've scrapped it altogether for `multipass` - it just works!

**Thoughts:** There will be so much to learn

---

## Day 59, November 30, 2019

**Today's Progress:** Successfully ran my first kubernetes cluster on my macbook today. Using k3s, and multipass to create linux VMs; so excited for my RPi to arrive so the home lab comes even more real.

**Thoughts:**

---

## Day 60, December 1, 2019

**Today's Progress:** Spent the majority of the day getting my day-zero ducks in-a-row for setting up a k8s cluster once my RPi arrives. Three general steps:

1.  flash my OS on the SD card
2.  fire-up the RPi, and prep it as the `master` node
3.  provision a few VMs, and add to the cluster
    Also took advantage of the cyber Monday deals for the CNCF & Linux Foundation's partnership on the CKA training / exam. Yes!!

**Thoughts:**

---

## Day 61, December 2, 2019

**Today's Progress:** Have my RPi 4 online; though with only one board I'm trying to create one or two VMs. `multipass` isn't playing nice with `qemu`. Looking into virtualisation for Ubuntu on Raspberry Pi.

**Thoughts:**

---

## Day 62, December 3, 2019

**Today's Progress:** After two days of solving unexpected, nested issues; I have my RPi running Ubuntu Server 19.10 running VMs via KVM, Qemu, and a Ubuntu iso installed by virt-installer. Now watch multipass releases a fix for `qemu` tomorrow ^.^

**Thoughts:**

---

## Day 63, December 4, 2019

**Today's Progress:** Installed a fan for the Raspberry Pi, and put the unit in a case. The case isn't great - the board doesn't line up perfectly with the port holes; the SD card is a bit tight. It's booting, and running fine though.

Finished reading Chatper 2 material for CKA training

**Thoughts:**

---

## Day 64, December 5, 2019

**Today's Progress:** Have `k3s` installed on my master and VMs - though the server is "refusing to connect". I think I've forgotten to disable `swap`. Will trouble shoot the details tomorrow.

Hot tip - copy files from a host to a VM with the `scp` command: e.g.

```bash
scp localfile.xyz user@<VMs IP addr>:/destin/ation/path
```

**Thoughts:** I haven't spent this much time at the CLI since installing Arch on a Dell XPS 13 with a Broadcom wireless card ^.^

---

## Day 65, December 6, 2019

**Today's Progress:** Still stuck on server refusing to connect, after ensuring swap was disabled. Missing the clues at the moment.

**Thoughts:**
