# Scene - center? pivot?

&#x20;Scene 탭에 보면 이상한 게 있다.

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

&#x20;옆에 Global, Local은 유니티의 공간 모드를 전역으로 할 것인지, 내가 고른 오브젝트 중심으로 할 것인지 하는 이름만큼 이해하면 되는건데 Pivot은 퀵소트 때 말고 들은 적이 없는 생소한 단어라서 와닿지 않았다. 요것은 조작 핸들, 흔히 기즈모(Gizmo, 뭐시기, 아무튼 이라는 뜻)를 띄우는 방식이다.

&#x20;pivot은 **오브젝트의 실제 기준점**을 기준으로, 센터는 **눈에 보이는 중점**을 기준으로 배치한다. 이것을 이해하기 위해서 Cube 자식으로 Sphere 하나 놓아보았다. 그리고 먼저 Center의 경우,

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

두 물체의 중점 부근이 나타나게 된다. 또 신기한 사실이 있는데, 만약 Cube가 0, 0, 0이고 Sphere가 2, 0, 0인 상태로  Cube의 자식으로 넣었다고해보자. 이때 Cube를 -2, 0, 0으로 하면 마찬가지로 구도 평행이동을 실시한다. 근데 이러면 0, 0, 0이 아니라 이상한 값이고 알고보니 자식으로 넣는 순간 좌표가 이상해진다는 것을 알 수 있다. 그 이유는 자식으로 넣는 순간 부모가 전역 좌표계가 되고 위에 보면 Cube가 약간 틀어져 있기 때문에 축 평행이동이 이상하게 적용되는 것이다. 정리하면 아래와 같다.

1. 지역 공간에서 위치, 회전, 스케일링 : 부모 오브젝트 기준으로 측정(지역 공간)
2. 지역 공간에서 평행이동 : 오브젝트 자신의 방향을 기준으로 평행이동.

글 써놓고 보니 참 와닿지 않고 재미 없는 것 같다 흠

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>

&#x20;pivot은 참고로 위 사진 처럼 Cube가 Sphere라는 자식을 가져도 시각적인 중심을 갖게 된다. 아까 center일 때에는 Sphere를 가지고 있어서 그 사이 부근에 기즈모가 찍힌다.
