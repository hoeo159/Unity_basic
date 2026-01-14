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
