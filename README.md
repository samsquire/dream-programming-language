# dream-programming-language

This is the repository for my unnamed dream programming language and runtime.

# context

I am a backend and devops engineer. I usually reach for Python to develop small programs to see how to implement something, then Java for multithreaded programs and C or Java for my own programming language implementation projects. I wrote the beginnings of an amd64 JIT compiler in C at https://github.com/samsquire/compiler. I also worked describing algebralang https://github.com/samsquire/algebralang.

# my dream

* But I want some language that helps me program and think but deliver ready-for-production quality and level solutions.
* The language helps you think of things from a data orientated perspective.
* I want linear scalability.
* I want to write distributed systems, performant and multithreaded asynchronous backends as easily and reliably deployable as a PHP app. Go is probably fit for this purpose, but I want to model how I think in my language.
* Everything is nonblocking in my dream programming language. Blocking is handled by the compiler and runtime.
* I think the language should have persistable pipelines or state machines as a first class concept like Temporal.io and support extremely fast messaging between threads.
* It should parallelise by default.
* A built-in advanced resolution algorithm that removes classes of bugs and handles all overrides and configuration potentialities. Configuration is easy.
* I want a programming language that I can think in and has a notation that is effective for solving the kinds of problems that I have.

* I want programs written in this language to be linearly scalability from day 1 without additional effort.
* easy concurrency, parallelism, async and coroutines

* high performance
* easy to write

desired features and characteristics

# example programs

## sharding and paralellisation

Imagine we want to download a URL, parse it, fetch links and save it.

We have 12 threads and we want to keep all the following tasks running in parallel, with maximum use of resource.

```
task download-url
	for url in urls:
		download(url)

task extract-links
	parsed = parse(document)
	return parsed

task fetch-links
	for link in document.query("a")
		return link

task save-data
	db.save(url, link)
```

This should have this grid:

![schedule]()![Slide2](C:\Users\samue\dream-programming-language\Slide2.PNG)



Programs are mixtures of parallel state machines and imperative logic.

## bank example - start transaction generator threads and send money between accounts

```
main = { generate_transactions }
	   { handle_transactions } # these go on in parallel
	   
handle_transactions = transaction(amount, source_account, destination_account)
	 | enough(source_account, amount) deduct(source_account, amount) credit(destination_account, amount)
handle_transactions = transaction(amount, source_account, destination_account)
	| !enough(source_account, amount) reject
    
def generate_transactions():
	while (true) {
		destination_account = rng.nextInt(accounts.size())
		source_account = rng.nextInt(accounts.size())
		amount = rng.nextInt(accounts.get(source_account).balance)
		fire transaction(amount, source_account, destination_account)
	}



def enough(source_account, amount):
	return balances[source_account] >= amount

def credit(destination_account, amount):
	balances[destination_account] += amount
	
def deduct(source_account, amount):
	balances[source_account] -= amount
```

The compiler knows when things change and refresh logic shall regenerate facts when they become true.

# first class coroutines and wiring

We can make forward references, to avoid being forced to move code around problems.

```
producers = []

task Producer():
	while running:
		output.yield(1)

task Consumer():
	while running:
		value = input.read()
		print(value)

for index in range(0, 10):
	producers = Producer()
	producers.append(producer)
	producer.output -> consumer.input

consumer = Consumer()

multiple_consumers = []
one_producer = Producer()
for item in range(0, 10):
	consumer = Consumer()
	multiple_consumers.append(consumer)
	one_producer.output -> multiple_consumers

```

I really like the ideas in [quaint lang](https://github.com/bbu/quaint-lang).

# website flow machine

```
homepage | category-page | products-listing | product-page | add-to-basket | checkout | checkout-sign-in | delivery-details | payment-details | place-order | confirmation
```



* 

# thoughts about what a programming language should do

* a language that calls deliberate attention to what you're trying to do
* a language that abstracts implementation details away from architectural details and allows the architecture to be independently transformed over time without breaking implementations
* a language that allows easy migration of data structures over time
* a language that allows the construction of super reliable, robust programs
* a language that doesn't cause sprawl of low signal files, symbols
* a language that densely packs meaning, without boilerplate but without too many complicated features
* a language that represents collections of observable behaviours as a first class citizen
* a language that allows existing behaviours to be customised
* a language that allows behaviours to be interleaved
* a language that has a straightforward behavioural debugging system
* a language that solves memory management
* a language with extreme reproducibility
* a language that is as reliable as PHP, once it's deployed it stays running, doesn't crash
* a language as reliable as Erlang, software failures don't crash the entire application

# beautiful async runtime

* functions are effectively concurrent processes.
* The granularity of tasks should be as small or as large as you want.

* State machines and async are combined together.

* Flowcharts

* Error flowcharts



# state machines and 

It's possible to check if your code is compatible based on types and the standard cycle

Behavioural progressions are defined upfront and composable.

# circular and steady state machines

The compiler enforces that state machines are monotonic. That the right form of new information always creates a new state and moves the state machine forwards. This gives us extreme power:

* to detect if a state machine becomes stuck - if no events of the right kind can possibly be raised to advance the state machine, then the state machine cannot progress, we can use control flow analysis to detect this stuckness. This is reachability analysis.
* if a state machine state is no longer reachable, then that's an error situation
* tie state machines together to indicate that they should work in lockstep (one causes the other)

The language can do a compile time check to ensure that your state machine can always make progress. 

```
taker:
item_available(i) = process_item(i) | return_item(i)
publisher:
generate_item(i) = item_available(i)
```



# behavioural debugging

State gets in the way of behaviours. 

# log focus

In this language, there is a primitive that allows you to narrow down log lines displayed to particular debug lines.
