# rigidbody.AddForce()

이동을 할 때에는 꾹 누르기 때문에 isPressed를 쓰지만 점프 같이 한 번 누르는 동작들은 AddForce를 이용해 rigidbody에 힘을 순간적으로 가해야 한다.

```
rigidbody.AddForce(Vector3, ForceMode)
```

Vector3는 당연히 방향과 크기가 들어갈 것이고 ForceMode에는 어떤게 있을까??

1.  Force(default)

    짧은 시간에 지속적으로 가속하는 크기로 Update 처럼 계속 호출할 때 쓰는 것. 질량에 영향을 받는다.
2.  Acceleration

    이거는 Force 처럼 지속적인 힘이지만 질량 상관없이 일정한 힘을 받게 한다.
3.  Impulse

    한 번에 주어지는 힘으로 질량에 영향을 받는다.
4.  VelocityChange

    질량에 영향을 받지 않은 순간적인 힘이다.



대개 캐릭터나 그런 거에 무게가 있는 디테일한 점프면 Impulse를 쓰는게 좋을 것 같다. Acceleration은 뭔가 쓰려면 이걸 잘 알아야 잘 쓸 수 있을 것 같다.
