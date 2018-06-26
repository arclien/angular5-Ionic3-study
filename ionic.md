# Ionic3

## Provider
앱의 UI는 여러 페이지로 구성. 각 페이지에서 실행되어야 할 작업은 각 페이지의 ts에 정의된 클래스에 해당 작업을 정의해서 사용.
페이지가 로딩 될 때는 해당 페이지의 클래스 객체가 생성되어 작업 실행. 필요에 따라 동일 페이지에 여러 객체를 생성 가능

만약, 모든 페이지에서 공통으로 사용되는 작업은 어떻게 할까?
예를들어 사용자의 아이디를 모든 페이지에서 보여준다고 하면, 모든 페이지에서 객체를 만들어서 매번 처리할 수는 없다. 이 때 한번 입력 받은 아이디를 저장한 후
모든 페이지에서 가져와서 사용하면 해결이 된다. 이 때 사용하는 기능이 Provider이다.

Provider는 말 그대로 제공자이다. 다른 객체들이 같이 사용하는 단 하나의 객체가 필요할 때 이를 싱글톤인 Provider로 정의할 수 있다.

```
app.module.ts
...
entryComponents: [
  MyApp
],
providers: [
  StatusBar,
  SplashScreen,
  MyCustomDataProvider,
]
...

```
entryComponents에 선언된 class의 객체는 필요시 자동으로 생성되며 둘 이상 생성되기도 함.
Providers에 선언된 class객체는 앱 구동 시 하나 생성되며, 다른 객체에서 접근 가능하다.
이와 같은 provider객체의 생성은 DI( Dependency Injection )이라고 부른다.
MyCustomDataProvider와 같이 만들어서 사용하는 provider은 반드시 app.module.ts파일에 privoders 섹션에 추가해야 사용 가능하다.


```
my-custom-data.ts
...
@Injectable()
export class MyCustomDataProvider{

  myData:string = "Sin Prisa Pero Sin Pausa";
  
  constructor(){
    console.log("It's raining");
  }
  
  getMyData(){
    return this.myData;
  }
}
...
```
@Injectable 데코레이터를 통해 DI를 정의해준다.
앱 구동 시 생성되는 Provider 객체는 각 페이지의 constructor 파라미터로 받는다.

```
home.ts
...
export class HomePage{
  myData:string;
  constructor(
    public navCtrl: NavController,
    myCustomDataProvider: MyCustomDataProvider
  ){
    this.myData = myCustomDataProvider.getMyData();
  }
}
...
```
```
home.html
...
<ion-header>
  <ion-navbar>
    <ion-title> {{myData}} </ion-title>
  </ion-navbar>
</ion-header>
...
```

모든 앱에서 공통으로 사용되는 작업이나 데이터에 대해 provider를 통해 코드의 재사용상을 높이고 코드 관리를 쉽게 할 수 있다.
특히 data consistency가 된다.


## NavController
page는 NavController객체를 constructor에서 파라미터로 받을 수 있다.
NavController은 페이지의 history를 관리하며 페이지 객체의 array로 구성.
페이지 이동은 push,pop을 통해 이루어짐.

```
next.ts
@component({
  selector: 'page-next',
  templateUrl: 'next.html',
})

export class NextPage {
  constructor(
    public navCtrl: NavController,
    public navParams: NavParams
   ){}
   
   moveToPrevPage(){
    this.navCtrl.pop();
   }
 ...
 
}
```

NavController은 push/pop을 통해 페이지의 life cycle과 관련된 이벤트를 발생시킨다.

### 기본 life cycle 이벤트
- ionViewCanEnter()
  - page의 constructor이후 호출. 페이지가 보여지기 전 페이지 진입 가능 여부 확인 가능.
  
- ionViewDidLoad()
  - page Load될 때 불리는 함수. 페이지 초기화 코드 정의. page constructor에서는 컴포넌트들이 생성되기 전이나, 여기에서는 이미 컴포넌트들이 생성되어 참조 가능하다.
  
- ionViewWillEnter()
  - 페이지가 보여지기 전 호출
  
- ionViewDidEnter()
  - 페이지가 보여진 후 호출
  
- ionViewCanLeave()
  - 페이지가 사라지기 전에 나갈 수 있는지 확인 가능.
  
- ionViewWillLeave()
  - 페이지가 가려지기 전 호출

- ionViewDidLeave()
  - 페이지가 가려진 후 호출

- ionViewWillUnload()
  - 페이지가 삭제되기 전 호출
