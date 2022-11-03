---
layout: post
title: Swift String vs Substring
subtitle: split()
categories: Swift PS
tags: Swift PS
---

알고리즘 문제를 풀다 보면 split() 함수로 문자열을 나누어 저장해야 하는 경우가 많다.

split() 함수의 원형은 아래와 같이 생겼는데
```swift
extension BidirectionalCollection where Self.SubSequence == Substring {

    /// Returns the longest possible subsequences of the collection, in order,
    /// around elements equal to the given separator.
    ///
    /// - Parameter separator: A regex describing elements to be split upon.
    /// - Returns: A collection of substrings, split from this collection's
    ///   elements.
    public func split(separator: some RegexComponent, maxSplits: Int = .max, omittingEmptySubsequences: Bool = true) -> [Self.SubSequence]
}
```
기본적으로 구분자(separator)를 인자로 받고 최대로 나눌 문자열의 갯수를 maxSplits, 빈 문자열을 무시할 것인지 여부를 omittingEmptySubsequences 인자로 받는다.

그 결과로 배열에 담긴 Substring 이 리턴된다.

그럼 String 과 Substring 에는 무슨 차이가 있을까

## Substring
기본적으로 문자열을 쪼개면 Substring 을 얻게 되는데 Substring 은 String 과 큰 차이가 없지만 성능상의 이점을 얻기 위해 원본 String 의 메모리를 공유하는 새로운 객체이다.

따라서 원본에서 메모리를 복사해오는 등의 추가적인 연산이 필요 없게 되어 성능에서 이점을 받게 된다.

Substring 은 String(_ :) 이니셜라이저로 String 으로 형변환이 가능하고 이 경우엔 새로운 메모리를 할당받아 String 객체가 생성되는 것으로 보인다.
```swift
let str = "Hello World!"
let subStr = str.split(separator: " ") // ["Hello", "World!"]
let subStrToStr = String(subStr[0]) // "Hello"
```

※주의점

Substring은 원본 String 을 참조하므로 연산이 수행되는 범위를 벗어나서 저장되지 않도록 주의해야 한다. 알고리즘 문제를 풀면서는 그다지 주의할 필요는 없지만 원본 String 의 전체를 참조하고 있기 때문에 원본을 참조하는 다른 변수가 없더라도 Substring 이 저장되어 있다면 메모리 누수를 유발할 수 있게 된다.
>Don’t store substrings longer than you need them to perform a specific operation. A substring holds a reference to the entire storage of the string it comes from, not just to the portion it presents, even when there is no other reference to the original string. Storing substrings may, therefore, prolong the lifetime of string data that is no longer otherwise accessible, which can appear to be memory leakage. -https://developer.apple.com/documentation/swift/substring
