# Angular Component Advanced
- 컴포넌트는 독립된 스코프를 가진 하나의 완결된 뷰를 그리는 요소
- 로직과 CSS가 해당 컴포넌트 안에서만 유효
- 객체 지향 방식으로 컴포넌트를 만들면 적합하다.
- 각각의 객체가 서로 상태를 주고 받으며 메서드를 호출하며 애플리케이션을 구성.

## Component?

### 웹 컴포넌트
- 위에 정의한 컴포넌트 정의와 달리, 브라우저에서는 컴포넌트에 독립적인 환경을 허용하지 않는다.
- 즉, 컴포넌트가 아닌 페이지 단위로 DOM을 읽고 js, css 정보를 페이지 단위로 적용 및 공유한다.
- 그래서 Custom Elements, HTML Imports, Template, Shadow DOM 4개의 기술 스펙으로 이루어진 웹 컴포넌트라는 표준이 생겼다.
- Custom Elements : 브라우저 HTML 표준에 명시되지 않는 요소.
- Template : 화면에 렌더링되지 않지만 동적으로 렌더링할 수 있는 template요소.
- Html Imports : HTML페이지 안에서 다른 HTML을 불러올 수 있다.
- Shadow DOM : DOM트리 내에 독립적 환경의 새로운 DOM 트리를 구축하여 자식 요소를 포함시킬 수 있다.
  - 유튜브에서의 video 요소
  - 재사용 가능한 UI를 독립적인 하나의 요소로 캡슐화
  ![Shadow DOM](shadow-dom1.png)
  ![Shadow DOM](shadow-dom2.png)

### 컴포넌트와 스타일 정보
- 어떻게 특정 컴포넌트에서만 유효한 스타일 정보를 제공할까?
- 앵귤러는 템플릿으로부터 생성된 DOM에 임의의 속성(attribute)를 추가시키고, css selector로 포함시켜 해당 컴포넌트에서만 유효하게 한다.
```
//my-ioslated-component.css
.my-isolated-component{
  display:block;
}

//실제 DOM 적용되는 css
.my-isolated-component[_ngcontent-c1] {
  display:block;
}
//실제 DOM
<div _ngcontent-c1 class="my-isolated-component"></div>
```

### 컴포넌트의 독립성을 깨는 안티패턴
- 컴포넌트는 독립적인 뷰를 통하여 외부에 노출시키지 않는다.
- 하지만 이는 앵귤러에서의 논리적인 설계일뿐, 실제 브라우저에서는 모두 볼 수 있고 접근도 가능하다.
- 즉, 하나의 페이지를 구성하는 두개 이상의 컴포넌트가 서로 DOM API( document.querySelector('span')등 )을 통해 서로 연결시킬 수 있다.
- 이러한 코드에는 DOM API라는 코드의 사용문제점과, 이로인한 두 컴포넌트 간의 높아진 결합도이다.
- 즉, 각가의 독립된 컴포넌트는 각각의 템플릿에서 로직을 작성하고 해당 뷰를 렌더링해야하는데, 두 개의 이론적으로 무관한 컴포넌트가 서로의 로직과 뷰에 관계를 맺기 때문에 지양해야할 패턴이다.
- jQuery를 사용하여 dom이 렌더링 된 후에 접근하여 조작하는 일을 지양하자.

## 컴포넌트 간 상태 공유와 이벤트 전파
- 독립된 컴포넌트를 만들지만, 실제 웹 애플리케이션에서는 이러한 컴포넌트가 거대한 트리로 구성되어 다른 컴포넌트와 상태 정보를 공유하거나 이벤트를 발생시킨다.

### 부모-자식 컴포넌트 간의 통신
- 부모-자식 관계를 갖는 컴포넌트 사이에는 프로퍼티 바인딩과 이벤트 바인딩으로 상호 작용 가능하다.
- input decorator을 통해 부모 컴포넌트의 상태 값을 자식 컴포넌트에 전달 가능하다.
- output decorator을 통해 자식 컴포넌트에서 부모 컴포넌트로 이벤트를 발생 가능하다.
```
//부모 컴포넌트의 view
<test-child [myAnotherState]="myState" [clonedVal]="uniqueVal" (onChangeChildData) ="receiveData($event)"></test-child>

//자식 컴포넌트의 로직
import { Component, Input, Output, EventEmitter } from '@angular/core';

@Component({ ... })
export class TestChildComponent {

  @Input() myAnotherState;
  @Input() clonedVal;
  @Output() onChangeChildData = new EventEmitter<number>();

  constructor() {}

  changeMyData() {
    const resultVal = 1111;
    this.onChangeChildData.emit(resultVal);
  }
}

//부모 컴포넌트의 로직
import { Component, Input, Output, EventEmitter } from '@angular/core';

@Component({ ... })
export class TestParentComponent {

  myState;
  uniqueVal;

  constructor() {}

  receiveData(resultVal) {
    console.log("자식으로 부터 받은 데이터 ",resultVal);
  }
}
```