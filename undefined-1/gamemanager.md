# GameManager 만들기

&#x20;게임 매니저는 게임의 규칙과 게임 오버 상태 작게는 하나의 씬의 상태, 플레이어 등 게임의 전체적인 것들을 다루는 중요한 것이다. 그렇다보니 여러 라이브러리에서 함수들을 빌려오고 임포트하는 일이 비일비재한데 이럴 때에는 천재적인 사고보다 아는 게 힘이다!는 것을 알 수 있다. 따라서 요 부분은 GameManager 하면서 알게되는 라이브러리와 각종 도구들을 정리하는 공간이 되지 않을까?

`UnityEngine.UI` : 유니티 UI 시스템과 관련된 코드

`UnityEngine.SceneManagement` : SceneManager 등이 포함된 씬 관리 관련 코드 예를 들어 씬 재시작

1. `SceneManager.LoadScene(string sceneName)`

&#x20;스크립트 파일 제목도 바로 class로 들어가기 때문에 잘 지어줘야 한다. 다른 스크립트에서 꺼낼 때 해당 스크립트 클래스를 가진 객체를 하나 생성해야 하기 때문이다.

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption><p>대충 짜면 이렇게 짜치는 코드를 볼 수 있다;</p></figcaption></figure>

&#x20; 보니까 script 제목대로 컴포넌트 제목이 대문자에 맞게 띄어쓰기가 자동으로 되고 GameObject나 요런 것도 띄어쓰기가 잘되고 오타도 바로 보이고 이름을 참 잘 정해야 할 것 같다.

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>
