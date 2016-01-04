Swift Style Guide
=================

![Swift](https://img.shields.io/badge/Swift-2.1-orange.svg)

본 문서는 StyleShare 구성원들이 Swift 코드를 이해하기 쉽고 명확하게 작성하기 위한 스타일 가이드입니다. 구성원들의 의사결정에 따라 수시로 변경될 수 있습니다.

## 목차

- [코드 레이아웃](#코드-레이아웃)
    - [들여쓰기 및 띄워쓰기](#들여쓰기-및-띄워쓰기)
    - [줄바꿈](#줄바꿈)
    - [최대 줄 길이](#최대-줄-길이)
    - [빈 줄](#빈-줄)
- [네이밍](#네이밍)
    - [클래스](#클래스)
    - [함수](#함수)
    - [변수](#변수)
    - [상수](#상수)
    - [약어](#약어)
    - [Delegate](#delegate)
- [클로저](#클로저)
- [클래스와 구조체](#클래스와-구조체)
- [타입](#타입)
- [주석](#주석)
- [프로그래밍 권장사항](#프로그래밍-권장사항)

## 코드 레이아웃

### 들여쓰기 및 띄워쓰기

- 들여쓰기에는 탭(tab) 대신 4개의 space를 사용합니다.
- 콜론(`:`)을 쓸 때에는 콜론의 오른쪽에만 공백을 둡니다.

    ```swift
    let names: [String: String]?
    ```

- 연산자 오버로딩 함수 정의에서는 연산자와 괄호 사이에 한 칸 띄어씁니다.

    ```swift
    func ** (lhs: Int, rhs: Int)
    ```

### 줄바꿈

- 함수 정의가 최대 길이를 초과하는 경우에는 괄호를 기준으로 줄바꿈합니다.

    ```swift
    func collectionView(collectionView: UICollectionView,
                        cellForItemAtIndexPath indexPath: NSIndexPath) -> UICollectionViewCell {
        // ...
    }

    func animationControllerForPresentedController(presented: UIViewController,
                                                   presentingController presenting: UIViewController,
                                                   sourceController source: UIViewController)
                                                   -> UIViewControllerAnimatedTransitioning? {
        // ...
    }
    ```

- 함수를 호출하는 코드가 최대 길이를 초과하는 경우에는 파라미터 이름을 기준으로 줄바꿈합니다.

    ```swift
    let actionSheet = UIActionSheet(
        title: "정말 계정을 삭제하실 건가요?",
        delegate: self,
        cancelButtonTitle: "취소",
        destructiveButtonTitle: "삭제해주세요"
    )
    ```

    단, 파라미터 이름이 없는 첫 번째 파라미터는 첫 줄에 씁니다. 만약 이름이 없는 첫 번째 파라미터가 너무 길다면 줄바꿈해도 무방합니다.

    ```swift
    UIView.animateWithDuration(0.25,
        animations: {
            // ...
        },
        completion: { finished in
            // ...
        }
    )
    ```

- 변수 정의가 최대 길이를 초화가는 경우에는 적당한 위치에서 줄바꿈하고, 한 단계 들여쓰기합니다.

    ```swift
    let cell = tableView.dequeueReusableCellWithIdentifier(CellIdentifier.VeryVeryLongUser)
        as! UserCell
    ```


- `if let` 구문이 길 경우에는 `let`과 `where`를 기준으로 줄바꿈합니다.

    ```swift
    if let user = self.veryLongFunctionNameWhichReturnsOptionalUser(),
       let name = user.veryLongFunctionNameWhichReturnsOptionalName()
     where user.gender == .Female {
       // ...
    }
    ```

### 최대 줄 길이

- 한 줄은 최대 119자를 넘지 않아야 합니다.

    Xcode의 **Preferences → Text Editing → Editing**의 'Page guide at column' 옵션을 활성화하고 119자로 설정하면 편리합니다.

### 빈 줄

- 빈 줄에는 공백이 포함되지 않도록 합니다.
- 모든 파일은 빈 줄로 끝나도록 합니다.
- MARK 구문 위에는 두 줄의 공백을, 아래에는 한 줄의 공백을 둡니다.

    ```swift
    // MARK: Layout

    override func layoutSubviews() {
        // ...
    }


    // MARK: Actions

    override func menuButtonDidTap() {
        // ...
    }
    ```

## 네이밍

### 클래스

- 클래스 이름에는 UpperCamelCase를 사용합니다.
- 클래스 이름에는 접두사<sup>Prefix</sup>를 붙이지 않습니다.

### 함수

- 함수 이름에는 lowerCamelCase를 사용합니다.
- 함수 이름 앞에는 되도록이면 `get`을 붙이지 않습니다.

    **좋은 예:**

    ```swift
    func nameForUser(user: User) -> String?
    ```

    **나쁜 예:**

    ```swift
    func getNameForUser(user: User) -> String?
    ```

- Action 함수의 네이밍은 '주어 + 동사 + 목적어' 형태를 사용합니다.

    - *Tap(눌렀다 뗌)*은 `UIControlEvents`의 `.TouchUpInside`에 대응하고, *Press(누름)*는 `.TouchDown`에 대응합니다.
    - *will~*은 특정 행위가 일어나기 직전이고, *did~*는 특정 행위가 일어난 직후입니다.
    - *should~*는 일반적으로 `Bool`을 반환하는 함수에 사용됩니다.

    **좋은 예:**

    ```swift
    func backButtonDidTap() {
        // ...
    }
    ```

    **나쁜 예:**

    ```swift
    func back() {
        // ...
    }

    func pressBack() {
        // ...
    }
    ```

### 변수

- 변수 이름에는 lowerCamelCase를 사용합니다.

### 상수

- 상수 이름에는 lowerCamelCase를 사용합니다.

    **좋은 예:**

    ```swift
    let maximumNumberOfLines = 3
    ```

    **나쁜 예:**

    ```swift
    let kMaximumNumberOfLines = 3
    let MAX_LINES = 3
    ```

### 약어

- 약어는 항상 대문자로 표시합니다.

    **좋은 예:**

    ```swift
    let userID: Int?
    let HTML: String?
    let websiteURL: NSURL?
    let URLString: String?
    ```

    **나쁜 예:**

    ```swift
    let userId: Int?
    let html: String?
    let websiteUrl: NSURL?
    let urlString: String?
    ```

### Delegate

- Delegate 메서드는 프로토콜명으로 네임스페이스를 구분합니다.

    **좋은 예:**

    ```swift
    protocol UserCellDelegate: NSObjectProtocol {

        func userCellDidSetProfileImage(button: FollowButton)
        func userCell(button: FollowButton, didTapFollowButtonWithUser user: User)
        
    }
    ```

    **나쁜 예:**

    ```swift
    protocol UserCellDelegate: NSObjectProtocol {

        func didSetProfileImage()
        func followPressed(user: User)
        
        // `UserCell`이라는 클래스가 존재할 경우 에러 발생
        func UserCell(button: FollowButton, didTapFollowButtonWithUser user: User)

    }
    ```

## 클로저

- 파라미터와 리턴 타입이 없는 Closure 정의시에는 `() -> Void`를 사용합니다.

    **좋은 예:**

    ```swift
    let completionBlock: (() -> Void)?
    ```

    **나쁜 예:**

    ```swift
    let completionBlock: (() -> ())?
    let completionBlock: ((Void) -> (Void))?
    ```

- Closure 정의시 파라미터에는 괄호를 사용하지 않습니다.

    **좋은 예:**

    ```swift
    { operaion, responseObject in
        // ...
    }
    ```

    **나쁜 예:**

    ```swift
    { (operaion, responseObject) in
        // ...
    }
    ```

- Closure 정의시 가능한 경우 타입 정의를 생략합니다.

    **좋은 예:**

    ```swift
    ...,
    completion: { finished in
       // ...
    }
    ```

    **나쁜 예:**

    ```swift
    ...,
    completion: { (finished: Bool) -> Void in
        // ...
    }
    ```

- Closure 호출시 또다른 유일한 Closure를 마지막 파라미터로 받는 경우, 파라미터 이름을 생략합니다.

    **좋은 예:**

    ```swift
    UIView.animateWithDuration(0.5) {
        // ...
    }
    ```

    **나쁜 예:**

    ```swift
    UIView.animateWithDuration(0.5, animations: { () -> Void in
        // ...
    })
    ```

-  Closure 호출시 Closure를 유일한 파라미터로 받는 경우, 괄호를 생략해도 됩니다.

    ```swift
    let sortedArray = array.sort { ... }
    let sortedArray = array.sort() { ... }
    ```

- 하나의 구문만 존재하는 Closure 사용시 파라미터와 `return` 구문을 생략합니다.

    **좋은 예:**

    ```swift
    let sortedArray = array.sort { $0 > $1 }
    ```

    **나쁜 예:**

    ```swift
    let sortedArray = array.sort { obj1, objc2 in
        return obj1 > obj2
    }
    ```

## 클래스와 구조체

- 클래스와 구조체 내부에서는 `self`를 명시적으로 사용합니다.
- 구조체를 생성할 때에는 Swift 구조체 생성자를 사용합니다.

    **좋은 예:**

    ```swift
    let frame = CGRect(x: 0, y: 0, width: 100, height: 100)
    ```

    **나쁜 예:**

    ```swift
    let frame = CGRectMake(0, 0, 100, 100)
    ```

## 타입

- `Array<T>`와 `Dictionary<T: U>` 보다는 `[T]`, `[T: U]`를 사용합니다.

    **좋은 예:**

    ```swift
    var messages: [String]?
    var names: [Int: String]?
    ```

    **나쁜 예:**

    ```swift
    var messages: Array<String>?
    var names: Dictionary<Int, String>?
    ```

## 주석

- `///`를 사용해서 문서화에 사용되는 주석을 남깁니다.

    ```swift
    /// 사용자 프로필을 그려주는 뷰
    class ProfileView: UIView {

        /// 사용자 닉네임을 그려주는 라벨
        var nameLabel: UILabel!

    }
    ```


- `// MARK:`를 사용해서 연관된 코드를 구분짓습니다.

    Objective-C에서 제공하는 `#pragma mark`와 같은 기능으로, 연관된 코드와 그렇지 않은 코드를 구분할 때 사용합니다.

    ```swift
    // MARK: Init

    override init(frame: CGRect) {
        // ...
    }

    deinit {
        // ...
    }


    // MARK: Layout

    override func layoutSubviews() {
        // ...
    }


    // MARK: Actions

    override func menuButtonDidTap() {
        // ...
    }
    ```

## 프로그래밍 권장사항

- 가능하다면 변수를 정의할 때 함께 초기화하도록 합니다. [Then](https://github.com/devxoul/Then)을 사용하면 초기화와 함께 속성을 지정할 수 있습니다.

    ```swift
    let label = UILabel().then {
        $0.textAlignment = .Center
        $0.textColor = .blackColor()
        $0.text = "Hello, World!"
    }
    ```

- 상수를 정의할 때에는 `struct`를 만들어 비슷한 상수끼리 모아둡니다. 재사용성과 유지보수 측면에서 큰 향상을 가져옵니다. [CGFloatLiteral](https://github.com/devxoul/CGFloatLiteral)과 [SwiftyColor](https://github.com/devxoul/SwiftyColor)를 사용해서 코드를 단순화시킵니다.

    ```swift
    final class ProfileViewController: UIViewController {

        struct Metric {
            static let profileImageViewLeft = 10.f
            static let profileImageViewRight = 10.f
            static let nameLabelTopBottom = 8.f
            static let bioLabelTop = 6.f
        }
        
        struct Font {
            static let nameLabel = UIFont.boldSystemFontOfSize(14)
            static let bioLabel = UIFont.boldSystemFontOfSize(12)
        }
        
        struct Color {
            static let nameLabelText = 0x000000~
            static let bioLabelText = 0x333333~70%
        }

        // ...

    }
    ```

    이렇게 선언된 상수들은 다음과 같이 사용될 수 있습니다.

    ```swift
    self.profileImageView.frame.origin.x = Metric.profileImageViewLeft
    self.nameLabel.font = Font.nameLabel
    self.nameLabel.textColor = Color.nameLabelText
    ```

- 더이상 상속이 발생하지 않는 클래스는 항상 `final` 키워드로 선언합니다.

- 프로토콜을 적용할 때에는 extension을 만들어서 관련된 메서드를 모아둡니다.

    **좋은 예**:

    ```swift
    final class MyViewController: UIViewController {
        // ...
    }


    // MARK: - UITableViewDataSource

    extension MyViewController: UITableViewDataSource {
        // ...
    }


    // MARK: - UITableViewDelegate

    extension MyViewController: UITableViewDelegate {
        // ...
    }
    ```

    **나쁜 예**:

    ```swift
    final class MyViewController: UIViewController, UITableViewDataSource, UITableViewDelegate {
        // ...
    }
    ```

## 라이센스

본 스타일 가이드 문서는 CC-By 3.0 라이센스를 따릅니다. 자세한 내용은 [http://creativecommons.org/licenses/by/3.0/][http://creativecommons.org/licenses/by/3.0/] 링크를 참조해주세요.
