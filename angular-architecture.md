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


### @component 데코레이터
AppComponent 클래스 코드 위에 붙은 @Component는 앵귤러에 이 클래스가 컴포넌트임을 알리기 위함.
@는 데코레이터를 뜻한다.

컴포넌트 데코레이터를 통하여 앵귤러에 컴포넌트와 연결된 뷰 정도인 템플릿이나 스타일 정보등의 메타데이터를 전달 가능하다.
```
@Component({
    selector: 'app-root',
    templateUrl: './app.component.html',
    styleUrls: ['./app,component.css']
})
```
- selector : 'app-root' => 템플릿에서 컴포넌트를 나타내기 위한 태그를 의미한다. 
    - 이 예제에서는 AppComponent의 selector로 app-root로 선언했으므로, src/index.html을 보면 다음과 같이 선언되어 있을 것이다.
    - AppComponent의 뷰가 app-root 태그를 이용해서 뷰를 구성할 템플릿 코드가 바디에 삽입된다.
```
<body><app-root>Loading ...</app-root></body>
```
- templateUrl : 실제 이 컴포넌트의 뷰 템플릿 코드 위치
- styleUrls : 뷰 템플릿에 사용되는 css파일 위치.

## 컴포넌트 생명 주기
앵귤러는 뷰에 필요한  컴포넌트를 생성하고 다른 뷰로 전환하면서 사용하지 않는 컴포넌트를 소멸시키는 등 컴포넌트의 전체 생명 주기를 관리한다.


- ngOnInit
    - 실질적으로 컴포넌트가 초기화를 마치고 완전한 상태를 갖춘 시점 constructor는 ES6 클래스 문법 표준으로서 앵귤러가 초기화 작업을 수행하기 전이므로 컴포넌트의 속성 가운데 템플릿과 바인딩한 속성이나 부모 컴포넌트로 받은 속성 등의 초기화를 보장하지 않음
- ngOnDestroy
    - 컴포넌트가 뷰에서 제거되기 직전 호출
- ngAfterContentInit
    - 컴포넌트의 뷰가 초기화되는 시점에 호출, Content Projection으로 전달받은 템플릿의 초기화 완료 시점에 호출 됨
- ngAfterViewInit
    - 컴포넌트의 템플릿이 완전히 초기화된 시점에 호출; 이 시점에는 컴포넌트의 모든 속성이 정상적으로 바인딩되었고 뷰도 렌더링 되었음을 의미. 예를 들어 부모 컴포넌트로부터 프로퍼티 바인딩으로 받은 속성 a를 템플릿에서 뷰로 노출하도록 구현했을 때, ngAfterViewInit이 호출 될 때 a 속성은 부모 컴포넌트로부터 전달됐음을 보장하고 렌더링 됐다는 것도 보장.
- ngOnChanges
    - 어떠한 이벤트에 의해서 컴포넌트의 상태가 변경된다면 앵귤러는 ngOnChanges나 ngDoCheck를 호출; 구현한다고 반드시 호출되는 것은 아님
        -프로퍼티 바인딩을 통해 부모 컴포넌트에게 상태를 전달받은 경우에만 호출되는 메서드. SimpleChanges라는 인자와 함께 전달; SimpleChange 안에는 previousValue와 currentValue라는 속성과 isFirstChange라는 메서드로 이루어진 타입. 최초 호출 시: isFirstChange는 true, previousValue는 UNINITIALIZED, currentValue는 최초 바인딩 값.
- ngDoCheck
    - ngDoCheck는 앵귤러가 컴포넌트의 상태 변경을 감지한 후에 항상 호출. 기본적으로는 최초 컴포넌트 초기화 후 ngOnInit 이후 바로 호출. 이후에는 외부 이벤트에 따라 상태 변경 감지가 내부에서 실행된 후에 항상 호출 됨. 앵귤러가 변경 사항을 직접 관리하기 어려운 경우 구현해야 함, 가능하면 DOCheck를 구현하지 않거나 구현하더라도 무거운 작업을 포함시키면 안됨. 구현된 컴포넌트와 관계없이 애플리케이션에서 일어나는 모든 비동기 이벤트마다 호출되기 때문에 성능에 무리를 줄 수 있음.

## 컴포넌트 트리
하나의 뷰 템플릿가 여러개의 컴포넌트로 구성될 수 있다. 이럴 경우, 컴포넌트를 소유한 부모와 이 부모에 속한 자식 컴포넌트의 관계가 형성된다. 이를 통해 부모-자식 형태의 컴포넌트 트리가 구성.

## 데이터 바인딩
앵귤러는 데이터 바인딩을 통하여 뷰와 템플릿 사이에서 생긴 데이터의 변경을 자동으로 싱크해준다.
- 단방향 바인딩
    - 삽입식
        - {{userName}} // 컴포넌트에 선언한 속성을 뷰에 삽입하여 바인딩.
    - 프로퍼티 바인딩
        - DOM이 소유한 프로퍼티를 []로 바인딩
        - ``` <div [disabled]="isDisabled">ex</div> ```
    - 이벤트 바인딩
        - DOM의 이벤트 핸들러로 컴포넌트의 메서드를 사용.
        - ``` <div (click)="setChange('params')">aa</div> ```

- 양방향 바인딩
    
```
// html
<h4>
    <span>{{userName}}</span>님 헬로.
</h4>
<div class="contents">
    <label for="user-name">사용자 이름: </label>
    <input type="text" name="user-name" id="user-name" [(ngModel)]="userName" (ngModelChange)="onChange()">
</div>
// ts
onChange() {
    this.valid = this.userName.length > 0;
}
```
- input 요소에서 userName을 NgModel 지시자를 사용하여 양방향 바인딩.
- 이 값이 변경된 경우 ngModelChange를 통해 onChange메서드에 바인딩.//이벤트 바인딩
- input 요소에 입력된 값은 자동으로 컴포넌트의 userName 속성에 반영.// 삽입식




Referencing

조우진 (2017), Angular 첫 걸음, 한빛미디어, 서울

