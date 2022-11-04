---
layout: post
title: Swift 기본 자료구조 1
subtitle: Array
categories: Swift PS DS
tags: Swift PS DS
---

Swift 가 기본으로 제공하는 자료구조에는 Array, Dictionary, Set 3가지가 있다.

Array 에 대해 간략하게 알아보자.

※ 모든 자료구조는 구조체로 구현되어 있다 (= 값 타입이다.)

## Array
Array 는 이름 그대로 다른 언어의 배열과 유사한 기능을 한다. 대신 크기가 고정된게 아니라 C++ 의 vector 처럼 크기가 필요에 따라 조절된다.

Array 는 대괄호 [] 로 간편하게 선언할 수 있고 내부 요소의 타입은 적절하게 추론해준다.
```swift
    // An array of 'Int' elements
    let oddNumbers = [1, 3, 5, 7, 9, 11, 13, 15]

    // An array of 'String' elements
    let streets = ["Albemarle", "Brandywine", "Chesapeake"]
```
특정 타입의 빈 Array 를 만들고 싶다면 대괄호 안에 원하는 타입명을 넣어 선언한다.
```swift
    // Shortened forms are preferred
    var emptyDoubles: [Double] = []

    // The full type name is also allowed
    var emptyFloats: Array<Float> = Array()
```
특정 값으로 초기화 된 배열이 필요하다면 Array(repeating:count:) 이니셜라이저를 사용한다.
```swift
    var digitCounts = Array(repeating: 0, count: 10)
    print(digitCounts)
    // Prints "[0, 0, 0, 0, 0, 0, 0, 0, 0, 0]"
```

위에서 말했듯 Array 는 C++ 의 vector 와 유사하므로 원소를 맨 뒤에 삽입할 때는 O(1), 원소를 맨 앞에 삽입할 때는 O(n), 원소의 index 접근은 O(1), 원소의 탐색은 O(n), 중간에 있는 원소의 삭제는 O(n) 등의 특성을 가지고 있으므로 시간 복잡도에 주의해야 한다.

https://docs.swift.org/swift-book/LanguageGuide/CollectionTypes.html
