# IOS_Tip

[Lottie Animation](Tips/Lottie-Animation.md)

[Notification](Tips/Notification.md)

#### Closure

```swift
{ (parameters) -> returnType in
    statements
}  // 클로저의 기본 형태

let reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in
    return s1 > s2
})  // 인라인 클로저

// 파라미터, 리턴타입 생략
let reversedNames = names.sorted(by: { s1, s2 in return s1 > s2 } )

// return 생략
let reversedNames = names.sorted(by: { s1, s2 in s1 > s2 } )

// 후행 클로저
// 어떤 함수의 마지막 파라미터가 클로저라면 사용 가능
let reversedNames = names.sorted() {(s1: String, s2: String) -> Bool in
		return s1 > s2
}

// 함수의 파라미터가 하나의 클로저 밖에 없다면, () 생략 가능
let reversedNames = names.sorted {(s1: String, s2: String) -> Bool in
		return s1 > s2
}
```



#### 아무데나 터치해서 키보드 숨기기

https://kaushalelsewhere.medium.com/how-to-dismiss-keyboard-in-a-view-controller-of-ios-3b1bfe973ad1

