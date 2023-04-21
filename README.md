# dream-programming-language

This is the repository for my unnamed dream programming language.

# context

I am a backend and devops engineer. I usually reach for Python to develop small programs to see how to implement something, then Java for multithreaded programs and C or Java for my own programming language implementation projects. I wrote the beginnings of a amd64 JIT compiler in C at https://github.com/samsquire/compiler. I also worked describing algebralang https://github.com/samsquire/algebralang.

But I want some language that helps me program and think.

I want a programming language that I can think in and has a notation that is effective for solving the kinds of problems that I have.

I have decided to write example programs first and then explain the language.

# example programs

bank example

```
main = { generate_transactions} { handle_transactions }
handle_transactions = transaction(amount, source_account, destination_account)
	 ± amount > balance(source_account) deduct(source_account, amount) credit(destination_account, amount)
     
```



# high level goals

* a language that calls attention to what you're trying to do
* a language that abstracts implementation details from architectural details and allows the architecture to be independently transformed over time
* a language that allows easy migration of data structures over time
* a language that allows the construction of super reliable, robust programs
* a language that doesn't cause sprawl of low signal files, symbols
* a language that densely packs meaning, without boilerplate but without too many complicated sigils
* a language that represents collection of observable behaviours as a first class citizen
* a language that allows behaviours to be customised
* a language that allows behaviours to be interleaved
* a language that has a straightforward behavioural debugging system





# behavioural debugging

State gets in the way of behaviours. 

