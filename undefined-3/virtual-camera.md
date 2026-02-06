# Virtual Camera

#### Virtual Camear Parameter

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

1. Status : 현재 이 카메라가 Brain Camera가 지목하고 있는지? 그런 라이브 상태를 나타낸다. Solo 버튼을 누르면 강제로 이 카메라 화면만 볼 수 있다.
2. Save During Play : 말 그대로 play 중 camera를 수정하면 그걸 저장할 것인지 체크하는 것
3. Priority : 카메라가 여러 대 있을 때 누가 대장인지 정하는 Layer 계층과 같은 느낌이다. 10으로 설정하고 나중에 다른 Virtual Camera가 11짜리가 나타난다면 그 쪽으로 슥 넘어간다.
4. Follow, Look At : 각각 몸체의 이동과 고개 회전 방향을 나타낸다.
5. Lens
   1. Vertical FOV(Field of View) : 시야 각으로 클수록 광각, 작으면 망원 렌즈 역할을 한다.
6. Body : 카메라 몸체에 관한 세팅이다
   1. Binding Mode : 대상과 일정한 거리를 유지하는 모드. World Space는 전역 공간 기준으로 계산하겠다\~
   2. Follow Offset : 대상으로부터 떨어진 거리
   3. Damping : 카메라가 따라갈 때의 반응 속도, 텐션을 나타낸다. 0에  가까울수록 칼 같이 따라간다.
7. Aim : 카메라가 대상을 화면 어디에 둘지 결정
   1. Composer : 대상을 화면 안에 배치, dead zone, soft zone 등이 보인다.

