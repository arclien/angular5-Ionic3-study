# Service? why?
- 컴포넌트에서 비즈니스 로직을 분리
- 뷰, 컴포넌트에 관련 없이 애플리케이션 전역에서 사용 가능 => 반복 코드 줄임
- 서비스를 만들어서 필요한 컴포넌트에 dependency injection 시킴 by service method call

## service 생성과 사용
- 클래스로 선언
- 컴포넌트와 달리 @Component를 붙이지 않고, 주로 @Injectable을 붙인다.
- 단지 클래스를 선언하고 필요한 로직을 구현하여 가져다 쓰는게 전부

```
//CalculatorService
export class CalculatorService {
  add(a, b) {
    return a + b;
  }
  
  sub(a, b) {
    return a - b;
  }
  
  mul(a, b) {
    return a * b;
  }
  
  div(a, b) {
    return a / b;
  }
  
}
//이렇게 일반적인 사칙연산을 서비스로 만들어 분리해서, 모든 애플리케이션에서 dependency injection을 통해서 컴포넌트&뷰로부터 분리해서 사용 가능해진다.
```

```
//컴포넌트에서 서비스 사용
...
import { CalculatorService } from '../calculator.service';

@Component({ ...})
export class CalculatorComponent {
  private resutl: number;
  private anotherResult: number;
  private calculator: CalculatorService;
  
  constructor() {
    this.calculator = new CalculatorService();
  }
  
  add(a, b) {
    this.result = this.calculator.add(a, b);
  }
  
  addAnother(a, b){
    this.anotherResult = this.calculator.add(a, b);
  }
}
// 이 예제는 간단해서 사실 서비스의 필요성을 못느낄 수 있다.
// 하지만 위 계산에서 입력 받은 파라미터 a,b를 출력하고, 그 결과를 연산 후에 출력을 해야하는 로직으로 바꾸면
// 우리는 단지 서비스의 add 메서드안에 각각의 콘솔 출력 코드를 넣으면 된다.
// 하지만 서비스를 사용하지 않을 경우, 컴포넌트에서 add, addAnother 메서드에 각각 콘솔 코드를 중복되게 넣어야 한다.
```

## Singleton Service
- 하나의 서비스를 각각의 여러 컴포넌트에서 사용하면, 서비스 코드를 수정하면 모든 컴포넌트에서 동일하게 적용된다
- 예를 들어, 서비스에 있는 멤버변수를 변경해서 모든 컴포넌트에서 동일하게 변경된 값을 사용하려 한다면 주의해야할 사항이 있다.
- 만약 각각의 컴포넌트에서 서비스 인스턴스를 생성했다면, 그 변경된 멤버변수는 해당 컴포넌트에서 사용하는 서비스 인스턴스에서만 변경이 된다. 즉, 하나의 서비스가 동일하게 애플르케이션 전역에서 적용되지 않는다.
- 이 문제를 해결하려면, 하나의 서비스 인스턴스를 만들어서 모든 컴포넌트가 공유하면 된다.
- 그 방법으로는, 간단히 AppComponent에서 서비스를 생성한 후 필요한 컴포넌트에 전달하면 된다.

## Dependency Injection
- 싱글턴 서비스에도 하나의 문제가 있다.
- 만약 컴포넌트가 수백개라면, 서비스가 필요할 때마다 컴포넌트에 인스턴스를 전달해야한다.
- 만약 기획의 변화로 서비스 생성자에 파라미터를 하나 더 추가해야한다면, AppComponent에서 Service를 의존하고 있으므로 코드를 수정해야한다.
- 그러기에 dependency Injection을 통해서 이러한 문제를 해결 가능하다.
- 앵귤러에 인스턴스 생성에 필요한 정보를 선언하고, 필요한 시점에 그 인스턴스를 주입받기만 하면된다.
- 의존성 주입을 하면 싱글턴을 유지하기 위해 AppComponent에 서비스 인스턴스를 생성하지 않아도 되고, 필요에 따라 앵귤러 의존성 주입을 하면 동일한 인스턴스를 주입해준다.

```
//import 생략
import { MySpecialLoggerService } from './my-special-logger.service';

@NgModule({
  declarations: [...],
  imports: [...],
  providers: [MySpecialLoggerService],
  bootstrap: [AppComponent]
})
```

```
constructor( private logger: MySpecialLoggerService) {}
//이렇게 생성자의 매개 변수로 서비스를 주입한다.
```





