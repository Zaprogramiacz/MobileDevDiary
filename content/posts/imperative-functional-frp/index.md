---
title: 'Imperative, Functional, Functional Reactive: Do you know the difference?'
date: 2025-02-25
tags: ['Swift', 'Combine', 'Functional Reactive Programming']
cover: 
  image: 'images/cover.png'
  alt: 'Do You Know the Difference Between Imperative, Functional, and Reactive Programming?'
---

# Paradigms

## Imperative

In the imperative approach, we have a sequence of instructions that describe step by step how the program's state is modified.

Let's look on the example ⤵️

```swift
var value = 0

func increment() {
    value += 1 // Mutating the state
}

print(value) // 0
increment()
print(value) // 1
```
In the code we have a mutable variable `value` and a function `increment` that mutates the state (`value`). We first print the initial value, then increment it, and finally print the updated value.

Simple, right? Let's jump into functional programming!

## Functional

What is functional programming? Is it only about writing functions? 🤔

Not really.

Of course, functions are a foundation of functional programming, but they need to follow an important rule ⤵️

In functional programming, functions must not have side effects.

What's the side effect? - A side effect occurs when a function modifies any state outside of its own scope.

Looking at the imperative programming example, we can clearly see a side effect inside the increment function ⤵️

```swift {hl_lines=[4]}
var value = 0

func increment() {
    value += 1 // Mutating the state (Side effect)
}

print(value) // 0
increment()
print(value) // 1
```

How can we re-shape this code to align with functional programming principles? - we need to get rid of state mutation both from main program flow and inside the `increment` function. 

Let's fix the function first by passing the state (`value`) as an argument and returning the result of the operation as function's output.

```swift
var value = 0

func increment(_ value: Int) -> Int {
    value + 1
}

print(value) // 0
value = increment(value)
print(value) // 1
```

Now, `increment` is a pure function. It returns a new state by adding 1 to the input without mutating any external state. To manage state changes in functional programming, we create new values instead of modifying the old state.

Having pure functions always returning the same output for a given input makes them easier to test and debug.

Now we focus on mutability which functional programming aims to avoid. Instead of mutating the state - `value`, we transform the old state and return a new one.

The code refactored to the functional form ⤵️

```swift
func increment(_ value: Int) -> Int {
    value + 1
}

let initialState = 0
let incrementedState = increment(initialState)

print(initialState) // 0
print(incrementedState) // 1
```

By adding the `increment` method as an extension to `Int`, we can use method chaining to apply multiple transformations in a clean, readable way. This is a common practice in functional programming, known as function or method composition ⤵️

```swift
extension Int {
    func increment() -> Int {
        self + 1
    }
}

let initialState = 0
let incrementedState = initialState
    .increment()
    .increment()

print(initialState) // 0
print(incrementedState) // 2
```

## Functional Reactive

functional reactive programming is a paradigm that combines functional programming with publisher and subscriber pattern. It emphasises streams of events carrying data that can be transformed along the way to the subscriber. FRP enables better handling of concurrency and asynchronous operations, making code more expressive.

If we’d like to showcase the above example using FRP, it would look something like this ⤵️

```swift
var incrementSubject = PassthroughSubject<Void, Never>()
var valueSubject = CurrentValueSubject<Int, Never>(0)

let disposableStream = Publishers.CombineLatest(incrementSubject, valueSubject)
    .map { _, value in value + 1 }
    .subscribe(valueSubject)


print(valueSubject.value) // 0
incrementSubject.send()
print(valueSubject.value) // 1
```

### Final Thoughts

Having a deeper understanding of FRP, beyond just describing use cases like observing keyboard input to trigger requests, can truly make you stand out in an interview. The ability to explain the differences and principles behind Combine or RxSwift will position you as a more senior candidate in the eyes of the interviewer.

# Quiz

{{< include-quiz "imperative_functional_frp.md" >}}

{{< footer >}}
