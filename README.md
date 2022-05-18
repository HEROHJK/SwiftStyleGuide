Swift Style Guide
=================

github [StyleShare](https://github.com/StyleShare/swift-style-guide) 가이드를 기준으로 작성 됨.

최종 수정일 : 2022-05-18


# 목차
- [Swift Style Guide](#swift-style-guide)
- [목차](#목차)
- [현황](#현황)
- [StyleGuide용 라이브러리](#styleguide용-라이브러리)
- [Style Guide](#style-guide)
  - [코드 레이아웃](#코드-레이아웃)
    - [최대 줄 길이](#최대-줄-길이)
    - [들여쓰기 및 띄어쓰기](#들여쓰기-및-띄어쓰기)
    - [줄 바꿈](#줄-바꿈)
    - [빈 줄](#빈-줄)
  - [네이밍](#네이밍)
    - [클래스 / 구조체](#클래스--구조체)
    - [함수](#함수)
    - [열거형](#열거형)
    - [약어](#약어)
  - [클로저](#클로저)
  - [클래스 / 구조체](#클래스--구조체-1)
  - [타입](#타입)
  - [주석](#주석)
- [프로그래밍 권장사항](#프로그래밍-권장사항)
- [SwiftLint 사용 가이드](#SwiftLint-사용-가이드)


# StyleGuide용 라이브러리

* ### [SwiftLint](https://github.com/realm/SwiftLint)
    * 컨벤션 강제 도구
* ### [Then](https://github.com/devxoul/Then)
    * 이니셜라이징 개선용 코딩 스타일 개선 라이브러리


# Style Guide

## 코드 레이아웃

### 최대 줄 길이

* 한줄은 100자를 넘지 않도록 함.
    * 원래 120자였는데.. 소형 모니터에서 왼쪽 브라우저를 연 상황에서 120자까지 표시되지 않음.
    * Xcode의 **Preferences -> Text Editing -> Display**의 **Page guide at column** 에서 100으로 설정.

### 들여쓰기 및 띄어쓰기

* 콜론(`:`)을 쓸 때에는 콜론의 오른쪽애만 공백을 둠.
* 단, 삼항 연산자의 경우 앞뒤로 띄움.

```Swift
    let name: String
    let result = one > other ? true : false
```

* 연산자 오버로딩 함수 정의에서는 연산자와 괄호 사이에 한칸의 공백 필요.

```Swift
    func ** (one: Int, other: Int)
```

### 줄 바꿈

* 함수의 정의가 최대 길이를 초과하는 경우, 파라미터를 기준으로 줄 바꿈.

```swift
    func collectionView(
      _ collectionView: UICollectionView,
      cellForItemAt indexPath: IndexPath
    ) -> UICollectionViewCell {
      // doSomething()
    }

    func animationController(
      forPresented presented: UIViewController,
      presenting: UIViewController,
      source: UIViewController
    ) -> UIViewControllerAnimatedTransitioning? {
      // doSomething()
    }
```

* 함수 호출 코드 또한 위와 같음.

```swift
    let actionSheet = UIActionSheet(
      title: "정말 계정을 삭제하실 건가요?",
      delegate: self,
      cancelButtonTitle: "취소",
      destructiveButtonTitle: "삭제해주세요"
    )
```

* 파라미터에 클로저가 2개 이상 존재하는 경우에는 무조건 내려쓰기.

```swift
    UIView.animate(
      withDuration: 0.25,
      animations: {
        // doSomething()
      },
      completion: { finished in
        // doSomething()
      }
    )
```

### 빈 줄
* 빈 줄에는 공백이 포함되지 않도록 함.
* 모든 파일은 빈 줄로 끝나도록 함.
* MARK 구문의 위와 아래에는 공백이 필요.
```Swift
// MARK: Layout

override func layoutSubviews() {
  // doSomething()
}

// MARK: Actions

override func menuButtonDidTap() {
  // doSomething()
}
```

## 네이밍
### 클래스 / 구조체
* 약어는 네이밍의 가장 첫번째를 제외하고는, 대문자로 처리
  * 변수명이 `id`같은 경우에만 소문자로 처리
* 이름에는 UpperCamelCase를 사용.
  * 약어는 예외로, 대문자 처리
* 클래스 이름에 접두사를 붙이지 않음.
  * 파생형의 앞자리등의 접두사를 붙이지 않음.

```Swift
/// 좋은 예
class ViewController: ActionViewController { }
/// 나쁜 예
class AViewController: ActionViewController { }

/// 좋은 예
let userID
let id
user.secondID = "test2"
/// 나쁜 예
let userId
let iD
user.secondId = "test2"
user.secondid = "test2"
```

### 함수
* 함수 이름에는 lowerCamelCase를 사용.
* 함수이름에는 되도록이면 get, set같은 명칭을 쓰지 않으며, 클래스 메소드인 경우 이름이 중복되지 않도록 처리.
* 매개변수 또한 되도록 간단한 접두사를 이용하여 처리.

```Swift
/// 좋은 예
func name(for user: User) -> String?
func grade(from: Subject) -> User?
/// 나쁜 예
func getName(user: User) -> String?
func getGradeFromSubject(subject: Subject) -> User?
```

### 열거형
* enum의 각 case에는 lowerCamelCase를 사용.

```Swift
/// 좋은 예
enum Result {
    case success
    case failure
}

/// 나쁜 예
enum Result {
    case Success
    case Failure
}
```

### 약어
* 약어의 경우, 시작은 똑같이 소문자로 표기하나, 시작이 아닌 경우 무조건 대문자로 표기.
```Swift
/// 좋은 예
    let userID: String
    let html: String
    let websiteURL: URL
    let urlString: String
/// 나쁜 예
    let userId: String
    let HTML: String
    let websideUrl: URL
    let URLString: String
```

## 클로저
* 파라미터와 리턴타입이 없는 Closure 정의 시, () -> Void를 이용.
* Closure 정의 시 파라미터에는 괄호를 사용하지 않음.
* Closure 정의 시 가능한 경우 타입 정의 생략, 사용하지 않는 파라미터 또한 `_` 로 표기
* 호출 시 마지막 파라미터가 Closure인 경우 파라미터 이름 생략.
```Swift
/// () -> Void의 예
/// 좋은 예
let completion: (() -> Void)?
/// 나쁜 예
let completion: (() -> ())?
let completion: ((Void) -> (Void))?

/// 괄호 관련 예
/// 좋은 예
{ operation, response in

}
/// 나쁜 예
{ (operation, response) in

}

/// 타입 정의 관련 예
/// 좋은 예
{ _, result -> Void in
    print(result)
}
/// 나쁜 예
{ (statusCode: Int, result: JSON) -> Void in
    print(result)
}

/// 마지막 파라미터
/// 좋은 예
UIView.animate(withDuration: 0.5) {
    // doSomething
}
/// 나쁜 예
UIView.animate(withDuration: 0.5, animations: { () -> Void in
    // doSomething
})
```

## 클래스 / 구조체
* 클래스와 구조체 내부에서는 self를 명시적으로 사용.
* 구조체를 생성할 때에는 Swift 구조체 생성자를 사용.
  * build, make같은 메서드 사용 지양

## 타입
* `Array<T>`, `Dictionary<T: U>` 보다는 `[T]`, `[T: U]`를 사용.

## 주석
* `///`를 사용하여 문서화에 사용되는 주석 남김.
* `// MARK:`를 사용하여 연관 코드 구분.


# 프로그래밍 권장사항
* 가능하다면 변수를 정의할 때 함께 초기화. 이때 Then을 이용.
```Swift
/// 좋은 예
let label = UILabel().then {
    $0.textAlignment = .center
    $0.textColor = .black
    $0.text = "Hello, World"
}
/// 나쁜 예
let label = UILabel()
label.textAlignment = .center
label.textColor = .black
label.text = "Hell World"
```

* extension은 되도록 분리.
```Swift
/// 좋은 예
class ViewController: UIViewController {
    // ...
}

// MARK: - 테이블뷰 Extension

extension ViewController: UITableViewDataSource {
    // ...
}

extension ViewController: UITableViewDelegate {
    // ...
}

// MARK: - 콜렉션뷰 Extension

extension ViewController: UICollectionViewDataSource {
    // ...
}

extension ViewController: UICollectionViewDelegate {
    // ...
}
/// 나쁜 예

class ViewController: UIViewController, UITableViewDataSource, UITableViewDataSource, UICollectionViewDataSource, UICollectionViewDelegate {
    // ...
}
```

# SwiftLint 사용 가이드
* [SwiftLint](https://github.com/realm/SwiftLint)를 먼저 설치
* xcode 프로젝트 스크립트에서, 아래 스크립트를 추가.
```bash
if which swiftlint >/dev/null; then
  swiftlint
else
  echo "warning: SwiftLint not installed, download from https://github.com/realm/SwiftLint"
fi
```

* M1의 경우
```bash
if test -d "/opt/homebrew/bin/"; then
  PATH="/opt/homebrew/bin/:${PATH}"
fi

export PATH

if which swiftlint >/dev/null; then
  swiftlint
else
  echo "warning: SwiftLint not installed, download from https://github.com/realm/SwiftLint"
fi
```
* 프로젝트에 .swiftlint.yml 파일을 만든 후, 아래 코드 추가
* `parent_config: https://raw.githubusercontent.com/HEROHJK/SwiftStyleGuide/master/lint.yml`
