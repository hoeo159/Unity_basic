# Animator 관련 코드

&#x20;이전 [animator](animator.md) 관련 지식이나 [IK](../undefined-2/fk-ik.md) 관련 내용을 대충 알면 좋다. IK 문서에서 쓴 예시를 다시 써보자면 물건을 집을 때 FK는 어깨 > 팔 > 손 순서대로 움직인다면 IK는 손 > 팔 > 어깨 순서대로 명령을 실행하게 된다. 우리가 지금 할 것은 총이 상체에 붙어서 함께 움직이면서 반동같은 자연스러운 움직임을 구현하는 것이 목표이다.

&#x20;하지만 FK 방식으로는 총의 위치를 보고 상체를 붙일 수 없기 때문에 IK 방식으로 총의 위치에 맞게 손(자식 조인트)의 위치를 강제로 고정시키고 팔과 어깨(부모 조인트)가 알아서 꺾이는 방식으로 해야한다. 따라서 Player Shooter로 총을 관리하는 스크립트에서는 `OnAnimatorIK()`를 통해 이를 구현해야한다. `OnAnimatorIK()`는 animator component에서 IK 정보가 갱신될 때마다 전송되는 message이다.

```
public Transform gunPivot; // 총 배치의 기준점
public Transform leftHandMount; // 총의 왼쪽 손잡이, 왼손이 위치할 지점
public Transform rightHandMount; // 총의 오른쪽 손잡이, 오른손이 위치할 지점

private void OnAnimatorIK(int layerIndex) {
    // 총을 상체와 함께 흔들기
    // 캐릭터의 양손을 총의 양쪽 손잡이에 위치시키기
    gunPivot.position = playerAnimator.GetIKHintPosition(AvatarIKHint.RightElbow);

    // IK를 사용하여 왼손의 위치와 회전을 총의 왼쪽 손잡이에 맞추기
    playerAnimator.SetIKPositionWeight(AvatarIKGoal.LeftHand, 1.0f);
    playerAnimator.SetIKRotationWeight(AvatarIKGoal.LeftHand, 1.0f);

    playerAnimator.SetIKPosition(AvatarIKGoal.LeftHand, leftHandMount.position);
    playerAnimator.SetIKRotation(AvatarIKGoal.LeftHand, leftHandMount.rotation);

    // 이번에는 오른쪽
    playerAnimator.SetIKPositionWeight(AvatarIKGoal.RightHand, 1.0f);
    playerAnimator.SetIKRotationWeight(AvatarIKGoal.RightHand, 1.0f);

    playerAnimator.SetIKPosition(AvatarIKGoal.RightHand, rightHandMount.position);
    playerAnimator.SetIKRotation(AvatarIKGoal.RightHand, rightHandMount.rotation);
}
```

&#x20; 위 코드를 한 줄씩 분석해보자.&#x20;

```
gunPivot.position = playerAnimator.GetIKHintPosition(AvatarIKHint.RightElbow);
```

&#x20;gunPivot은 gun의 위치를 가지는 transform 타입의 오브젝트이다. animator component의 `GetIKHintPosition()`메서드는 `AvatarIKHint` 타입으로 부위를 입력받아 해당 부위의 현재 위치를 가져온다. 따라서 총의 위치를 캐릭터의 팔꿈치 위치로 순간이동 시키는 코드이다. `AvatarIKHint` 타입은 IK 대상 중 다음 부위를 표현하는 타입이다.

* `AvatarIKHint.LeftElbow`
* `AvatarIKHint.RightElbow`&#x20;
* `AvatarIKHint.LeftKnee`
* `AvatarIKHint.RightKnee`

&#x20;이어서 다음 줄

```
playerAnimator.SetIKPositionWeight(AvatarIKGoal.LeftHand, 1.0f);
playerAnimator.SetIKRotationWeight(AvatarIKGoal.LeftHand, 1.0f);
```

&#x20;캐릭터의 왼손의 위치와 회전을 `leftHandMount`의 위치와 회전으로 변경한다. `1.0f`는 weight에 대한 가중치 값이다. 이번에는 Hint가 아니라 `AvatarIKGoal` 타입이 나왔는데 다음 부위를 표현한다.

* `AvatarIKGoal.LeftHand`
* `AvatarIKGoal.RightHand`
* `AvatarIKGoal.LeftFoot`
* `AvatarIKGoal.RightFoot`

&#x20;가중치는 해당 부위의 원래 위치와 IK에 의한 목표 위치 사이에서 실제로 적용할 중간값을 결정하는 것이다. 예를 들어 0.5라면 원래 위치와 IK 목표 위치가 절반씩 섞여 사용된다. 그 다음 줄

```
playerAnimator.SetIKPosition(AvatarIKGoal.LeftHand, leftHandMount.position);
playerAnimator.SetIKRotation(AvatarIKGoal.LeftHand, leftHandMount.rotation);
```

&#x20;왼손 IK의 목표 위치와 목표 회전을 `leftHandMount`의 위치와 회전으로 지정한다. animator의 위 메서드는 IK 대상이 사용할 목표 위치와 목표 회전을 설정한다. 적용할 IK 대상은 왼손 `AvatarIKGoal.LeftHand`, 목표 위치는 총의 왼손 손잡이의 위치인 `leftHandMount.position`, 목표 회전은 왼손 손잡이의 회전인 `leftHandMount.rotation`이다. 오른손도 같은 방식으로 IK를 적용한다.

&#x20;쉽게 정리하면 위 코드는 다음과 같은 방식으로 적용한다

1. Animation이 재생됨(캐릭터가 달리기 동작 등을 함)
   1. 애니메이션을 다 계산한 직후에 조인트를 꺾기 위한 message를 보냄(`OnAnimatorIK()`)
2. 총의 위치(gunPivot)을 내 오른쪽 팔꿈치 위치로 순간이동 시킨다
   1. 총의 위치를 캐릭터에게 붙이는 동기화 작업
3. Unity Animator Component에게 허락 맡기
   1. 왼손의 position과 rotation을 조정할 것이라고 Set하기
   2. 가중치는 1.0, 100%로 변하는 IK 값을 반영하기
4. 실제로 왼손을 총의 왼손 목표 지점(`leftHandMount`)으로 이동시키고 회전시키기
5. 오른손에도 설정하기
