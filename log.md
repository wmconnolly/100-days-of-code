# 100 Days Of Code - Log

### Day 0: October 2, 2019

**Today's Progress**: Today I've made the decision to launch into the often seen '100 days of code' challenge, with the goal of learning `Go`; a language that is relatively new to me. After choosing the book _"Go in Action"_ I've settled on the following approach to the 100 days challenge: Read the book, explore the corresponding code (locally), and document my takeaways each day. If I end up with self-written code from a particular day, I'll post that too; though that may not be a frequent outcome. Otherwise, today I've setup vim-go, read up to page 94 (that includes readings before starting the challenge), and put this repository in motion! 

**Thoughts:** What's impressing me most from Go so far is what _it lacks_, or at least what it contstrains (i.e. formatting). From my perspective this is awesome, because as a new learner I feel my ramp-up time will be relatively quicker compared to that of a looser language, where there's a 'yes, do this; but...' to seemingly every aspect of the language. The only 'batteries included' aspect I see in Go, so far, is in its concurrency considerations - I am very excited by this, and feel the work done by the authors / core team will open up a sphere of programming that would otherwise be too prohibitive for my (current) non-professional relationship to computer science. A language which effectively handles events which may or may not depend on eachother, or to happen simultaneously is just _really really_ cool; no wonder Go has emerged as foundational tool for IT infrastructure. For day 1, I'll probably take a look at Go's type system, and reproduce some notes on that. 

--------

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