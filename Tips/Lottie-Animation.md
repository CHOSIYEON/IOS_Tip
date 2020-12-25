# IOS_Tip

### [Lottie Animation]

```bash
// Cocoapod 설치
sudo rm -rf /Library/Developer/CommandLineTools
sudo xcode-select --install
sudo gem install cocoapods -n /usr/local/bin

// lottie-ios 설치
pod init
sudo vi Podfile  // Podfile 에 pod 'lottie-ios' 추가
pod install      //후 xcode 재실행

```

```swift
// Swift 예제
import UIKit
import Lottie

class MainViewController: UIViewController {
    
    var titleLabel: UILabel = {
        let label = UILabel()
        label.textColor = .black
        label.textAlignment = .center
        label.font = UIFont.boldSystemFont(ofSize: 70)
        label.text = "메인 화면"
        return label
    }()
    
    let animationView: AnimationView = {
        let animView = AnimationView(name: "41401-merry-christmas")
        animView.frame = CGRect(x: 0, y: 0, width: 400, height: 400) // 크기
        animView.contentMode = .scaleAspectFill  // 이미지 확대 방식
        return animView
    }()
    
    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view.
        
        view.backgroundColor = .black
        view.addSubview(animationView)
        animationView.center = view.center
        
        
        
        // 애니메이션 실행
        animationView.play { (finish) in
            // 애니메이션 끝나면 콜백
            print("애니메이션 끝")
            // closure 안에서는 self 필수
            self.view.backgroundColor = .white
            self.animationView.removeFromSuperview()  // 애니메이션 지우기
            
            self.view.addSubview(self.titleLabel)
            self.titleLabel.translatesAutoresizingMaskIntoConstraints = false
            self.titleLabel.centerXAnchor.constraint(equalTo: self.view.centerXAnchor).isActive = true
            self.titleLabel.centerYAnchor.constraint(equalTo: self.view.centerYAnchor).isActive = true
        }
    }
}
```