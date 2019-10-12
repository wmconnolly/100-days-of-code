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
