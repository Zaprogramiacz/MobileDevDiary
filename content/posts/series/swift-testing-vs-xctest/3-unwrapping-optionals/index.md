---
title: '#3 XCTest vs. Swift Testing - Unwrapping optionals'
date: 2024-11-21
tags: ['Swift', 'XCTest', 'Swift Testing', 'unit testing', 'Testing']
series: "XCTest vs. Swift Testing"
cover: 
  image: 'images/cover.png'
  alt: '#3 XCTest vs. Swift Testing - Unwrapping optionals'
---

Optionals are a core of Swift - we deal with them daily, both in production and testing code. Whether you write tests with XCTest or Swift Testing, unwrapping optionals is a common case.

In XCTest there is `XCTUnwrap` operator.

Swift Testing introduces `#require` macro.

Is there any difference between them? Not really! Both require the test function to handle exceptions and `try` keyword before.

Gif ⤵️

![Example](images/example.gif)

Code ⤵️

XCTest
```swift
func testNewYorkTimeZone() throws {
    let newYorkTimeZone = try XCTUnwrap(
        TimeZone(identifier: "America/New_York")
    )
    XCTAssertEqual(newYorkTimeZone.abbreviation(), "GMT-5")
    XCTAssertEqual(newYorkTimeZone.identifier, "America/New_York")
}
```

Swift Testing
```swift
@Test
func newYorkTimeZone() throws {
    let newYorkTimeZone = try #require(
        TimeZone(identifier: "America/New_York")
    )
    #expect(newYorkTimeZone.abbreviation() == "GMT-5")
    #expect(newYorkTimeZone.identifier == "America/New_York")
}
```

{{< footer >}}
