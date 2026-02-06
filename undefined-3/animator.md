# Animator

&#x20;Player 오브젝트는 기본적으로 [유한 상태 머신](../undefined-2/fsm.md)이다. 따라서 현재 상태는 하나의 상태만 될 수 있다. 하지만 여러 개의 FSM을 병렬로 실행하는 방식으로 여러 상태가 동시에 중첩되게 할 수 있다. Animator에서도 Layer를 여러 개 쌓음으로써 여러 애니메이션을 하나의 오브젝트에 중첩되게 할 수 있다.

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption><p>Player의 Animator</p></figcaption></figure>

&#x20;Layer 탭을 보면 Base Movement 레이어는 걷고 뛰는 기본 움직임에 Upper Body 레이어로 조준, 재장전 애니메이션을 덮을 수 있다. 이는 [아바타 마스크](undefined-1.md)에서 설정해줄 수 있다. 기본적으로 위에서 아래로 덮어쓰는 overridding 형식이기 때문에 순서에 주의하면 된다. Parameter에는 보통 애니메이션 정도를 위한 값, 다른 상태의 전이 조건을 위한 트리거 등으로 쓰인다.

#### Blend Tree

&#x20;예를 들어 Die라는 State에는 Die에 관한 모션을  나타내는  Animation Clip이 있다. 하지만 Animation Clip 외에도 특수한 종류의 모션을 상태에 할당하는 것이 가능한데 그 중 하나가 Blend Tree 모션이다.

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption><p>Blending Tree</p></figcaption></figure>

&#x20;Blend Tree는 여러 Animation Clip을 parameter에 따라 모션을 블랜딩해준다. 그림에서 보면 Move라는 수치에 따라 Run 부터 Walk, Idle까지 섞이게 되어 자연스럽게 변하게 된다. Blending Type을 2D로 변경하면 2개의 parameter를 쓰는 것도 가능하다.

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption><p>Parameter에 따른 Blending Tree</p></figcaption></figure>
