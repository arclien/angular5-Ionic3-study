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



# brew
맥OS에서 쉽게 패키지 관리를 돕는 도구.
[Home Brew](http://brew.sh) 에서 설치.
```
brew install node
// brew를 통해 node와 npm을 같이 설치 한다.
```


