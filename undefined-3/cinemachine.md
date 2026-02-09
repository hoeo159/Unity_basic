# Cinemachine

&#x20;Cinemachine은 카메라 연출을 위한 복잡한 수학적 모델과 수식을 대체해준다. 레이싱, FPS 등 다양한 장르마다 고유한 카메라 동작을 스크립트 없이 구현할 수 있다. Cinemachine이 제공하는 카메라는 크게 두 가지로 나뉜다.

* Brain Camera
* Virtual Camera

&#x20;Cinemachine의 카메라 추적을 구현하려면 우선 Brain Camera를 먼저 만들어야 한다. 이는 게임 월드를 촬영하는 현실 카메라이고 씬에 하나만 존재할 수 있다.

&#x20;[Virtual Camera](virtual-camera.md)는 실제 카메라로 동작하지 않지만 여러 parameter를 제공한다. Brain Camera가 특정 Virtual Camera를 activated camera로 설정하면 해당 위치로 이동한다. 또한 Virtual Camera의 여러 설정 값들을 입힐 수 있다. Brain Camera의 프리셋이나 shortcut 정도로 해석할 수 있다.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>Brain Camera 설정</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p>Virtual Camera 생성</p></figcaption></figure>

&#x20;Cine
