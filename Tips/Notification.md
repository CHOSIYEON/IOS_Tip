# [Notification]

```swift
// Notification 발송
// Name 은 Notification 을 구별할 수 있는 "이름"
// extension 을 활용
NotificationCenter.default.post(name: AddDiaryController.newDiary, object: nil)
```

```swift
// observer 가 반환하는 NSObjectProtocol 을 받아 사용하지 않을 때 제거 
var token: NSObjectProtocol?
    
    deinit {
        if let token = token {
            NotificationCenter.default.removeObserver(token)
        }
    }
```

```swift
override func viewDidLoad() {
        
        super.viewDidLoad()
        
        // Observer 등록
        // viewDidAppear() 은 UI update 사이클이 발동될때마다 호출 -> notification 이 여러번 호출 될 가능성 있음
        // 따라서 viewDidLoad() 에서 호출
        token = NotificationCenter.default.addObserver(forName: AddDiaryController.newDiary, object: nil, 
        queue: OperationQueue.main) {_ in
            self.reloadTableView()
            print("reload")
        }
        
    }
```
