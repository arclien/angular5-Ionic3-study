# angular5-study

## 앵귤러/리액트 사용하는 이유?
- 우선 각각 장단점, 목적이 다름.
- 프론트에서 하는게 많아져서 순수 JS, jQuery로 짜는데 한계가 생김. 코드 복잡해짐. 유지보수 힘듬
- Angular, React는 SPA(Single Page Application) 개발을 위한 프레임워크. // React는 라이브러리
- 프론트 코드(js,html,css,assets)등의 패턴화. 구조화. 컴포넌트 재사용. 아키텍쳐등을 위해 사용.

### ng new
```
ng new hello-angular
cd hello-angular
```

앵귤러 CLI로 프로젝트를 만들면 기본 스켈레톤 폴더가 생긴다.
- e2e 폴더 : End-to-End의미. protractor라는 툴을 사용하여 브라우저에서 테스트할 코드가 있다.
- src 폴더 : 실제 코드
- .angluar-cli.json : angular-cli에서 사용할 설정 정보
- karma.conf.js : Karma라는 단위테스트 도구 설정
- protractor.conf.js : e2e 통합 테스트를 위한 설정
- tslint.json : 타입스크립트용 구문 체크 설정
- tsconfig.json : 타입스크립트 컴파일 설정
- src/typings.d.ts : 타입스크립트에서 사용할 타입 선언 정보

### ng serve
프로젝트를 로컬에서 개발 환경으로 실행하는 명령. 
웹 서버 구동 후 Webpack을 통해 소스를 번들링.
localhost:4200에서 확인가능.




## Lists
- Typescript & ES6 Javascript.
  - [Quickstart 정리문서](https://docs.google.com/document/d/1F4xYbzDvnWzuLeVn6yTZ4ZuuQwsBP4InCjNWEEHWP2o/edit)
- Components & Binding
  - [Components 정리문서](https://docs.google.com/document/d/1JzgW9L9SMTE2CN896pu4QQlBQiDq_E5NI49GANLgWJE/edit)
- Directives
  - [Built-in 정리문서](https://docs.google.com/document/d/16xiGaH4VFyYN_FVsJ6Q1gWb2UMYxvOFQegUtvlD-CQI/edit)
  - [Custom 정리문서](https://docs.google.com/document/d/12RrV8NiKb7ZhpDjPSqOEYrShzxjVvdNJvo8-HvkYXeU/edit)
- Dependency Injection & Services
	
- Angular Modules & Bootstrapping your Angular application.

- SPAs & Routing

- Angular CLI

- Forms
	- [Angular - Reactive Forms](https://angular.io/guide/reactive-forms)
- Reactive Programming with RXJs
	- [RXJs 정리문서](https://docs.google.com/document/d/1lq_4U1hR_ajTVqL4wTgX4-0Y4bPm4rH7G-HGJpGky1o/edit)
- HTTP

- Testing

- Packaging & Releasing
- Pipes
	- [Pipe 정리문서](https://docs.google.com/document/d/1sJKgD2DZwDjUViEulWKwTYmjHc9wSLzaDj8d8qHLyls/edit)
## References
- [Differnece between Directives and Components](https://blog.angular-university.io/angular-components-and-directives-for-beginners/)

So it looks like the browser has this built-in feature that seems very useful for creating new HTML elements from existing ones. Using it we can:

- define a public XML-like API to an element of the page
- define the look and feel of the element using HTML
- we can add behavior to that new element
- we can even style it while keeping those styles isolated

This combined specification of a look and feel, an API and a behavior is a useful concept, so let's give it a name: let's call it a Directive. This new directive will be a very particular type of HTML Directive: more than behavior, it has also an associated look and feel. We will call to that type of Directive a Component - it's simply a Directive with a template.



We’ve touched on a few directives already, such as NgFor.
Directives are components without a view. They are components without a template. Or to put it another way, components are directives with a view.
				
Everything you can do with a directive you can also do with a component. But not everything you can do with a component you can do with a directive.



- [Decorators](https://toddmotto.com/angular-decorators)
  - [decorators](https://angular-2-training-book.rangle.io/v/v2.3/handout/features/decorators.html)
  - [property_decorators](https://angular-2-training-book.rangle.io/v/v2.3/handout/features/property_decorators.html)
  - [class_decorators](https://angular-2-training-book.rangle.io/v/v2.3/handout/features/class_decorators.html)
  - [parameter_decorators](https://angular-2-training-book.rangle.io/v/v2.3/handout/features/parameter_decorators.html)
  
- Service vs provider vs factory 
	- [Differences](https://www.linkedin.com/pulse/whats-difference-between-service-factory-provider-angularjs-kumar/)
	- [jsFiddle Demo](http://jsfiddle.net/pkozlowski_opensource/PxdSP/14/)
	- Factory: A factory is a simple function which allows you to add some logic before creating the object. It returns the created object.
	- Service: A service is a constructor function which creates the object using new keyword. You can add properties and functions to a service object by using this keyword. Unlike factory, it doesn’t return anything.
	- Provider: A provider is used to create a configurable service object. It returns value by using $get() function.
  - 
## 한국말 참고자료
- [Poiemaweb](https://poiemaweb.com/angular-basics)
- [Angular 강좌](https://moon9342.github.io/angular-lecture-introduction)
