# Unity6 키보드 입력 가이드



과거 방식은 Input Manager 방식으로 Input.GetKey( \~\~ )을 이용했다.

```
if (Input.GetKey(KeyCode.Space)) 
{
    // 점프
}
```

벝!

요즘은&#x20;

```
using UnityEngine.InputSystem;
if (Keyboard.current != null && Keyboard.current.spaceKey.isPressed)
{
    // 점프
}
```

이런 방식을 선택한다.&#x20;

또한 일반적인 선형 이동을 실행할 때에도 옛날에는 **rigidbody.velocity**를 이용했지만 지금은 **rigidbody.linearVelocity**로 **rigidbody.angularVelocity**와 잘 구분되게 쓰고 있다.

누르는 방식은 isPressed와 wasPressedThisFrame 크게 두 종류가 있다. wasPressedThisFrame은 Update의 짧은 시간 동안 처음 딱 한 번만 실행되도록 도와준다. 그래서 예를 들어 단축키로 UI를 키고 끌 때 한 번 눌렀는데도 미친듯이 깜빡거리는 오류를 방지할 수 있다. 아니면 자석축 키보드를 사야한다.
