# is trigger

&#x20;여기서부터 닷지 완성까지 만들었다가 merge 안하고 스트레이트로 달리다가 날라가버렸다... gitbook 아직 뭔가 불편하고 어렵다;;;;

&#x20;rigidbody와  Collider 컴포넌트를 보면 영어 단어들이 그냥 이름만 보고 아 이런 기능 하겠구나\~ 하겠는데 하나가 약간 헷갈렸다. 바로 `is trigger` 이라는 칸이다. player한테 활성화 시키면 그냥 바닥에 쑥 통과하여 떨어진다. is trigger의 기능은 약간 이게 물체가 아니라 센서처럼 동작하는 방식이다.

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption><p>탄알 충돌은 그냥 충돌 감지만 하면 된다!! 하고 게임 오버</p></figcaption></figure>

&#x20;기존에 트리거를 끄면 벽처럼 충돌과 동시에 감지가 가능하다. 근데 굳이 충돌 없이 플레이어가 접근했다는 정보만 필요하거나 플레이어가 모르는 무언가를 지나가게 하려고 할 때에는 충돌 기능 없이 왔다는 신호만 받을 수 있는 센서가 필요하다. 그래서 있는 게 `is trigger`이다. 이 이벤트가 발생하려면 충돌하는 두 물체 중 하나는 반드시 rigidbody 컴포넌트가 있어야 한다.

&#x20;Start나 Update에서 맨날 충돌을 감지하는 것은 정말 불편한 일이다. 마치 콜백함수처럼 뭔가 갱신될 때만 부르고 싶을 때에는 `OnTriggerEnter`를 사용한다. On\~을 이용한 Collision 계열은 총 세 가지 종류가 있다. 모두 OnColision\~이나 OnTrigger\~로 어미라고 하나??? 말 끝에 따라 다르다. 참고로 충돌 물체 중 trigger가 되어 있다면 OnTrigger를 써야한다.

1. OnCollisionEnter : 충돌한 순간
2. OnCollisionStay : 충돌하는 동안
3. OnCollisionExit : 충돌했다가 분리되는 순간
