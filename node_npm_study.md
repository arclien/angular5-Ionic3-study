# Node.js
Node.js는 이벤트 루프, 코어 라이브러리로 구성된 서버 사이드 자바스크립트 실행 환경.


# NPM
Node Package Manager이며 Node.js에서 기본으로 사용하는 패키지 관리 도구.
패키지 : 자바스크립트, HTML, CSS등을 포함한 리소스 묶음이며, NPM을 통해 공유 및 의존성 관리가 된다.

## NPM 명령어
- npm init : 명령이 실행되는 위치에 package.json을 만들어 NPM 패키지 관리 초기 작업 수행
- npm install : package.json파일이 있는 경우, 파일에 선언된 의존 패지키들을 설치.
- npm install <패키지명> : 해당 패키지를 내려받음 (ex, npm install jquery)
  - 추가적인 옵션으로 --save, --save-dev등을 사용 가능
- npm uninstall <패키지명> : 설치된 패키지 삭제.
- npm list : 현재 설치된 패지키 목록을 트리 형태로 보여줌
- npm run : package.json의 scripts에 선언된 명령을 수행.
- npm install -g : 글로벌 패키지에 추가하여, 현재 cli 폴더의 node_modules폴더가 아닌, 글로벌 폴더에 패키지를 설치하여 모든 프로젝트에서 사용 가능하다.
- npg install -save : dependencies 에 추가된다.

### NPM 실습
```
npm install jquery // 버전을 명시하지 않았으므로 최신 버전을 설치한다.
npm install jquery@1.12.4 // 1.12.4버전의 jquery를 설치한다.
```
package.json이 없이 특정 폴더에서 위 처럼 설치를 하면 터미널에 WARN과 package.json파일이 없다고 나온다.
WARN이라 설치는 정상적으로 되었다.

위 커맨드를 실행한 폴더 하위에 node_modules이라는 폴더가 생성되고 jquery패키지가 설치된다.
jquery 폴더를 보면 src와 dist폴더가 있고, src에는 jquery 소스전체가 있고 dist(distribution)폴더에는 배포용 소스가 있다.

### package.json
```
{
  "name": "Jay",
  "version": "0.0.0",
  "license": "MIT",
  "scripts": {
    "ng": "ng",
    "start": "ng serve",
    "build": "ng build",
    "test": "ng test",
    "lint": "ng lint",
    "e2e": "ng e2e"
  },
  "private": true,
  "dependencies": {
    "@angular/animations": "^5.0.0",
    "@angular/common": "^5.0.0",
    "@angular/compiler": "^5.0.0",
    "@angular/core": "^5.0.0",
    "@angular/forms": "^5.0.0",
    "@angular/http": "^5.0.0",
    "@angular/platform-browser": "^5.0.0",
    "@angular/platform-browser-dynamic": "^5.0.0",
    "@angular/router": "^5.0.0",
    "core-js": "^2.4.1",
    "jquery": "^3.3.1",
    "rxjs": "^5.5.2",
    "zone.js": "^0.8.14"
  },
  "devDependencies": {
    "@angular/cli": "1.5.0",
    "@angular/compiler-cli": "^5.0.0",
    "@angular/language-service": "^5.0.0",
    "@types/jasmine": "~2.5.53",
    "@types/jasminewd2": "~2.0.2",
    "@types/node": "~6.0.60",
    "codelyzer": "~3.2.0",
    "jasmine-core": "~2.6.2",
    "jasmine-spec-reporter": "~4.1.0",
    "karma": "~1.7.0",
    "karma-chrome-launcher": "~2.1.1",
    "karma-cli": "~1.0.1",
    "karma-coverage-istanbul-reporter": "^1.2.1",
    "karma-jasmine": "~1.1.0",
    "karma-jasmine-html-reporter": "^0.2.2",
    "protractor": "~5.1.2",
    "ts-node": "~3.2.0",
    "tslint": "~5.7.0",
    "typescript": "~2.4.2"
  }
}
```
- scripts : 프로젝트에서 실행할 커맨드들을 세팅하여 사용 가능하다. 특정 커맨드에 특정 스크립트 파일을 실행하게 한다거나, 실행 순서등등을 정의 할 수 있다.
- dependencies : 프로젝트에서 여러가지 패키지들을 사용(의존)한다. 오픈소스 패키지들이라서 버전이 계속 변하고 관리하기 힘들게 된다. package.json의 dependencies를 통해서 각 패키지들의 버전을 기록하고 해당 프로젝트에 맞게 버전을 기록하여, 새로운 버전에 대해 대처를 할 수 있게 한다. (실제로 프로젝트 진행하면서 moment 버전이 너무 빨리 변하며 deprecated된 함수가 많아서 문제가 생겨서, 버전업을 막은 경우도 있다 )
- devDependencies : 개발 환경에서만 의존하는 패키지를 정의한다. 실제 배포하기전에만 사용하는 웹팩을 넣어두고, 컴파일 후 실제 환경에는 컴파일 된 파일만 올리므로 웹팩은 dev에 넣는다.

- 버전 : 버전에는 메이저 / 마이너 / 패치 이렇게 세가지가 있으며, 각 패키지 버전의 숫자가 하나씩을 의미한다. 예를들어 
```
"jquery": "^3.3.1",
```
- 버전 : 여기에서 "^메이저(3).마이너(3).패치(1)"을 의미하며, 메이저는 이전버전과 호환이 안되는 대규모 업데이트 마이너는 이전버전 호환가능한 업데이트, 마지막으로 패치는 버그 수정시에 올린다.
- 기호 :  버전 앞에 올 수 있는 기호는 주로 기호 없음, ^, ~, 부등호가 있다.
  - 기호 없음 : 무조건 그 숫자의 버전을 설치
  - ^ : 마이너버전까지 변경을 허용 // 즉 jquery 3.x.x의 버전은 업데이트가 있으면 설치를 하지만, 4.x.x의 메이저 버전 변경은 막는다.
  - ~ : 패치버전까지 변경을 허용 // 즉 jquery 3.3.x의 버전은 업데이트 하지만, 3.x.x의 마이너 변경은 막는다.
  
* 오픈소스를 많이 가져다 쓰면, 버전이 신경쓰이고 버그를 유발한다. package.json을 잘 관리해야한다. 

# brew
맥OS에서 쉽게 패키지 관리를 돕는 도구.
[Home Brew](http://brew.sh) 에서 설치.
```
brew install node
// brew를 통해 node와 npm을 같이 설치 한다.
```


