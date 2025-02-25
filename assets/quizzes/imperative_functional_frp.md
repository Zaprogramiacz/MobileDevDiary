{{< quizdown >}}

---
primary_color: green
secondary_color: lightgray
text_color: black
shuffle_questions: false
shuffle_answers: true
---

# What is functional programming about?

1. [ ] Writing functions that may modify state as needed
1. [x] Avoiding side effects and state mutation
1. [ ] Relying on side effects to manage state transitions
1. [ ] Emphasizing object-oriented design patterns

# In functional programming, why must functions avoid side effects?

1. [ ] To improve performance
1. [x] To prevent unpredictable state changes
1. [ ] To enable state mutation
1. [ ] To allow recursion

# Which paradigm describes a sequence of instructions that modify the program’s state step by step?

1. [ ] Functional
1. [ ] Functional Reactive
1. [x] Imperative
1. [ ] Declarative

# What is considered a side effect in a function?

1. [ ] Returning a computed value
1. [x] Modifying a variable outside its scope
1. [ ] Calling another pure function
1. [ ] Using recursion

# How is state typically managed in functional programming?

1. [ ] By mutating global variables
1. [x] By transforming old state into new state
1. [ ] By ignoring state changes
1. [ ] By centralizing state in a single object

# Which pattern is used by functional reactive programming?

1. [ ] Singleton
1. [ ] Factory
1. [ ] Delegate and Callback
1. [x] Publisher and Subscriber

# What is the primary benefit of using pure functions?

1. [ ] They allow state mutations
1. [x] They are easier to test and debug
1. [ ] They increase code complexity
1. [ ] They require global variables

# Examine the code below. Does it fully follow the functional programming principles?

```swift
var value = 0

func increment(_ value: Int) -> Int {
    value + 1
}

value = increment(value)
print(value)
```
1. [ ] Yes, it's correct
1. [ ] No, the function has side effects
1. [x] No, it mutates state by reassigning a mutable variable
1. [ ] No, it mutates the "value" variable inside the increment function

{{< /quizdown >}}
