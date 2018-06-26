# Ionic3

## Provider
앱의 UI는 여러 페이지로 구성. 각 페이지에서 실행되어야 할 작업은 각 페이지의 ts에 정의된 클래스에 해당 작업을 정의해서 사용.
페이지가 로딩 될 때는 해당 페이지의 클래스 객체가 생성되어 작업 실행. 필요에 따라 동일 페이지에 여러 객체를 생성 가능

만약, 모든 페이지에서 공통으로 사용되는 작업은 어떻게 할까?
예를들어 사용자의 아이디를 모든 페이지에서 보여준다고 하면, 모든 페이지에서 객체를 만들어서 매번 처리할 수는 없다. 이 때 한번 입력 받은 아이디를 저장한 후
모든 페이지에서 가져와서 사용하면 해결이 된다. 이 때 사용하는 기능이 Provider이다.

Provider는 말 그대로 제공자이다. 다른 객체들이 같이 사용하는 단 하나의 객체가 필요할 때 이를 싱글톤인 Provider로 정의할 수 있다.