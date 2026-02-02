# Global Illumination

&#x20;글로벌 일루미네이션(Global Illumination, GI)이란 게 있다. 빛 반사가 어려운 이유가 광원 하나가 있더라도 물체 각각의 반사율, 알베도가 있기 때문에 2차 광원, 간섭광이 생긴다. 이것들을 GI라고 통칭하여 부르고 현실 세계는 이러한 2차, 3차, 4차 ... 가 포함된 간섭광들을 보기 때문에 실사 rendering에서는 필수적이다.

&#x20;trade-off로 매우 높은 부하가 걸리기 때문에 적당한 타협을 보는게 중요하다. 이것도 마찬가지로 고정된 오브젝트들에 대해 제한된다.

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption><p>Window-Rendering-Lighting-Realtime Lighting에 있습니다잉</p></figcaption></figure>

&#x20;우리가 만들 Lightmap처럼 미리 벽에 발라버린 것을 Baked GI, 움직이는 물체나 시간(밤/낮)에 따라 변경하는 것을 Realtime GI라고 한다. 흔히 아는 Ray Tracing이 이 부분을 계산한다. 근데 이 실시간도 미리 계산하는 정보들이 필요하기 때문에 Precomputed Realtime GI라고 부르기도 한다.

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

&#x20;Realtime Lighting 아래에는 Mixed Lighting이 있다. 이 모드들은 다음과 같다.

1. Baked Indirect
   1. 간접광만 구워서 미리 계산
   2. 직사광과 그림자는 실시간으로 처리
2. Subtractive
   1. 직사광, 간접광, 그림자까지 하나의 Lightmap에 구워버림
   2. 실시간 그림자와 미리 구워진 그림자가 자연스럽게 합성되진 않음
   3. 오버헤드가 가장 적다
3. Shadowmask
   1. 간접광을 위한 Lightmap + shadowmask map 추가 생성
   2. 실시간 그림자와 미리 구워진 그림자가 자연스럽게 합성됨

&#x20;여기서 **실시간 그림지와 미리 구워진 그림자가 합성된다**는 표현이 있다. 예를 들어보자면 당연히 플레이어는 실시간으로 빛을 계산해야한다. 근데 미리 구워진 나무 그늘에 플레이어가 걸어 들어간다면 플레이어 그림자가 나무에 닿자마자 없어지거나 따로 놀거나 blending이 잘 안되는 현상이 있다.

&#x20;좀 길어지는데 Light Component에도 비슷한 부분이 있다. 해당 light가 실시간으로 light effect를 반영할 것인지 또는 lightmap에 미리 구워서 사용할 것인지 정한다.

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

&#x20;Mode 부분에 볼 수 있는데 각 특징은 다음과 같다.

1. Baked
   1. 해당 light가 baked GI에 반영됨
   2. 특정 오브젝트에는 빛을 비추거나 그림자를 그릴 수 없음
      1. light를 굽는 시점에 없던 오브젝트
      2. 게임 도중 움직일 수 있는 동적 게임 오브젝트
   3. 런타임 도중 밝기나 색 변경 불가
2. Realtime
   1. 런타임에 설정이나 위치가 변경되면 오브젝트에 반영됨
   2. 실시간으로 움직이거나 생성되는 오브젝트의 그림자도 그릴 수 있음
   3. baked light에 비해 표현이나 그림자 질감이 떨어짐
3. Mixed
   1. 가볍거나 동적 게임 오브젝트에는 실시간, 무겁거나 정적 게임 오브젝트는 baked light
   2. 설정은 런타임에 변경 가능하지만 실시간으로 연산되는 것들만 반영됨(예를 들어 간접광은 반영 x)
   3.  baked GI의 세부 모드에 따라 조금씩 다르게 동작

       <figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

&#x20;참고로 GI는 정적(static) 오브젝트에만 적용된다!! 이건 게임 도중 위치가 변경될 수 없다
