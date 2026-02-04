# Player Rigidbody

#### Rigidbody Component

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

1. mass : 물체 무게, 충돌과 같은 물리현상에 대한 정도
2. Linear Damping :\
   &#x20;선형 감쇠로 이동할 때 받는 공기 저항, 마찰력 등, 0일 때는 마찰 없이 미끄러지 듯 이동한다.
3. Angular Damping : \
   &#x20;각 감쇠, 20으로 설정하여 충돌 등에 원치 않는 회전에 대해 내성을 가지게 했다.
4. Use Gravity : 중력의 영향
5. Is Kinematic : Check 일 때 물리 엔진의 힘을 무시한다
6. Interpolate : 움직임이 끊겨 보일 때 보간, 보정하는 기능
7. Collision Detection :\
   &#x20;충돌을 계산하는 방식으로 만약 총알처럼 빠른 물체가 뚫고 지나가는 현상이 발생한다면 Continuous로 바꿔야 한다.
8. Freeze Position : 특정 축으로 이동하지 못하게 막는다. Y가 위, 아래를 담당
9. Freeze Rotation : 회전을 고정하는 것으로 X, Z축을 고정하여 캐릭터가 앞, 뒤로 넘어지는 현상을 막음
10. Layer Overrides :\
    &#x20;충돌 관련해서 특별히 처리해줄 Layer가 있을 때 처리, Include는 강제로 닿을 수 있게 처리, \
    반대로 Exclude는 그냥 통과하도록 강제로 끄는 것

&#x20;보통 Rigidbody하고 Collider를 만들 때 사람 같은 Player는 Capsule Collider로 성능 향상을 노릴 수 있다.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>
