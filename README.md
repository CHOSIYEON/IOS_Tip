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



#### Navigation controller 에 값 전달하기

http://blog.naver.com/PostView.nhn?blogId=traeumen927&logNo=222010583912



#### ViewWillAppear

ViewController 가 최초로 실행 됐을 때, 다른 View로 가려졌다가 다시 보여졌을때 호출 된다.

iOS13 부터, 다른 ViewController를 present할 때 화면 전체를 채우는게 아니라 card 형태로 화면의 일부를 덮는 형태로 되기 때문에,

present된 View를 dismiss해도 ViewWillAppear()가 호출되지 않는다.

해결 방법: UIAdaptivePresentationControllerDelegate 사용

https://medium.com/better-programming/the-lifecycle-and-control-when-dismissing-a-modal-view-with-pagesheet-in-ios-13-4bbd1e3e1ec7

https://zeddios.tistory.com/828?category=682195



#### Delegate 를 이용해 ViewController간 값 전달

ViewController 끼리 데이터를 주고 받거나, 다른 ViewController의 함수를 실행하기 위해 delegate, protocol 사용하기
(Dismiss 할 때, 데이터를 전달 해주기 위해 사용)

class receiveVC: UIViewController / class sendVC: UIViewController 가 있다고 가정할 때, 
sendVC에서 데이터를 보내고, receiveVC 에서 받으려면

- sendVC에서 protocol 정의, delegate 변수 생성, protocol 함수 호출

  ```swift
  class sendVC: UIViewController {
    var sendVCDelegate: sendVCDelegate?
  
    func sendDataAndDismiss() {
      self.sendVCDelegate?.sendSomData(100)
      dismiss(animated: true)
    }
  }
  
  protocol sendVCDelegate {
    func sendSomeDate(data: Int) // 프로토콜 정의 시, 함수는 정의만 하고 구현하지 않는다
  }
  ```

- receiveVC에서 protocol 구현, delegate 지정 (sendVC를 present 할때)

  ```swift
  class receiveVC: UIViewController {
    func someAction() {
    	guard let controller = self.storyboard?.instantiateViewController(identifier: "sendVC") as? sendVC else 		{ return }
    	controller.sendVCDelegate = self
  	}
  }
  
  extension receiveVC: sendVCDelegate {
    func sendSomeDate(data: Int) {
      self.receive = data
    }
  }
  ```

  