---
title: "Swift Concurrency Riddle - TaskLocal"
date: 2025-05-17
tags: ['Swift', 'Swift Concurrency']
cover: 
  image: 'images/cover.png'
  alt: 'Swift Concurrency Riddle - TaskLocal'
---

## Intro

If you're able to solve this, it means you understand TaskLocal really well.

## Riddle

Look at the attached code snippet and guess:
- What will be printed at each step?
- Is the order of prints always the same?

```swift
class Riddler {
    @TaskLocal static var message = "Hello"

    static func riddleMe() {
        Self.$message
          .withValue("Bye", operation: {
              print("Print 1: \(Self.message)") // ???
              Task {
                  print("Print 2: \(Self.message)") // ???
              }
              Task.detached {
                print("Print 3: \(Self.message)") // ???
              }
          })
        print("Print 4: \(Self.message)") // ???
    }
}

Riddler.riddleMe()
```

### Hint
Do you want to learn more about TaskLocal and Test Scoping in Swift 6.1 first? - Check out my blog post on "Concurrency-Safe Testing in Swift 6.1 with TaskLocal and Test Scoping" [HERE](https://www.mobiledevdiary.com/posts/concurency-safe-testing-in-swift-6-1/).

## Answer

```swift
class Riddler {
    @TaskLocal static var message = "Hello"

    static func riddleMe() {
        Self.$message
          .withValue("Bye", operation: {
              print("Print 1: \(Self.message)") // Bye
              Task {
                  print("Print 2: \(Self.message)") // Bye
              }
              Task.detached {
                print("Print 3: \(Self.message)") // Hello
              }
          })
        print("Print 4: \(Self.message)") // Hello
    }
}

Riddler.riddleMe()
```

Console output
```swift
Print 1: Bye
Print 2: Bye
Print 3: Hello
Print 4: Hello
```

### Explanation
- **Print 1** - you're inside the `.withValue("Bye")` block. The message TaskLocal property is overriden bt "Bye"
- **Print 2** - the non-detached `Task { ... }` inherits the parent tasks's context, including TaskLocal override.
- **Print 3** - the detached task runs with a new context - it does not inherit any TaskLocal overrides.
- **Print 4** - outside the `withValue` block, the override reverts to the default "Hello" value

Is the order of prints always the same? - **No**

Why?

In the code snippet we spawn 2 tasks: a child Task and just after a dettached Task. Both run concurrently, so we have no control over when they start or complete. This means you can see the different output in the console for each code run.

{{< footer >}}
