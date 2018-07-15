# Architecture

## 앵귤러 : 사용자용 애플리케이션 개발을 위한 프레임워크
- 사용자용 애플리케이션 : 사용자가 애플리케이션을 사용하며 상호작용을 위한 매개로서 뷰를 만들어야한다.
- 프레임워크 : 애플리케이션을 모두 만들지 않고, 정해진 규칙에 맞추어 비즈니스 로직만 개발한다. 즉 사용자가 사용할 뷰와 연결된 로직을 개발.

```
ng new ng-welcome-msg-app
cd ng-welcome-msg-app
```

```
//ng-welcome-msg-app/src/app/app.components.html
//뷰를 구성할 마크업을 포함한 템플릿 파일
<h4>
    <span>{{userName}}</span>님 헬로~
</h4>
<div class="contents">
    <label for="user-name">사용자 이름 : </label>
    <input type="text" name="user-name" id="user-name" #nameInput>
    <button type="button" (click)="setName(nameInput.value)">입력</button>
</div>
```

```
//ng-welcome-msg-app/src/app/app.components.ts
//타입스크립트로 작성한 클래스
//컴포넌트는 기능이나 공통의 관심사를 기준으로 화면 하나를 여러 컴포넌트로 나누어 구성한다.
import  { Component } from '@angular/core';

@Component( { ... })
export class AppComponent {

    userName = '';

    setName(name) {
        this.userName = name;
    }

}
```
- {{userName}} : ts파일에 정의된 컴포넌트 클래스에 선언된 userName 속성 값을 html인 뷰에 반영.
- (click)="setName(nameInput.value)" : 뷰에서 클릭 이벤트가 발생할 때 클래스의 setName 메서드를 실행. 
- #nameInput : 뷰에서 #nameInput 속성의 선언된 input DOM 객체를 nameInput이라는 변수로 선언하여 사용.