---
title: '#4 XCTest vs. Swift Testing - Disable tests - handle with care'
date: 2024-11-27
tags: ['Swift', 'XCTest', 'Swift Testing', 'unit testing', 'Testing']
series: "XCTest vs. Swift Testing"
cover: 
  image: 'images/cover.png'
  alt: '#4 XCTest vs. Swift Testing - Disable tests - handle with care'
---

This week with Swift Testing starts with checking how test disabling differs from XCTest.

In XCTest, Xcode identifies a function as a test only if its name starts with the "test" prefix, so putting e.g. "disabled" instead makes the test inactive.
Swift Testing simplifies that approach by introducing the @Test macro with a `.disabled` trait that you can pass as an argument.

What’s the benefit? 
You no longer need to modify each test name to disable it. What’s more, you can include context directly within the trait to justify why the test is disabled.

Do I like it? You bet! I’m really glad that Xcode no longer depends on a "test" or other prefix 🥳

Na matter what’s the motive, your goal should always be to resolve it, because a disabled test does not provide any value to the project.

![Example](images/example.gif)

Code ⤵️

XCTest
```swift
// Disabled due to bug #12345
func disabled_testExampleTest() {
    XCTAssertEqual(1 + 1, 3)
}
```

Swift Testing
```swift
@Test(.disabled("Disabled due to bug #12345"))
func exampleTest() {
    #expect(1 + 1 == 3)
}
```

Why is "handle with care" mentioned in the title?
It’s simple - disabling a test it’s a rare situation and must always come with a good reason.
- Randomly failing test blocks a team from progressing - valid reason.
- Changes in the production code without updating tests - that should never happen.

{{< footer >}}
