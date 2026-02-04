# 공간 관련 퀴즈

&#x20;Sphere가 있고 Cube가 Sphere의 자식으로 들어가 있다. Sphere-Cube, Cube 이렇게 볼 수 있는데,

```
public Transform childTransform;

void Start()
{
    transform.position = new Vector3(0, -1, 0);
    childTransform.localPosition = new Vector3(0, 2, 0);
}
```

&#x20;코드를 보면 Sphere의 게임 오브젝트 위치는 0, -1, 0이고 자식인 Cube의 지역 위치는 0, 2, 0이다. 그리고 저 코드를 Sphere에 넣고 자식을 Cube에 넣고 실행한다. 실행 중에 일시적으로 수정해서 Cube를 자식 해제 하면 Cube의 위치는 어디에 찍힐까??

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption><p>정답</p></figcaption></figure>

```
    void Update()
    {
        if(Keyboard.current != null && Keyboard.current.upArrowKey.isPressed)
            transform.Translate(new Vector3(0, 1, 0) * Time.deltaTime);
        if(Keyboard.current != null && Keyboard.current.downArrowKey.isPressed)
            transform.Translate(new Vector3(0, -1, 0) * Time.deltaTime);
        if(Keyboard.current != null && Keyboard.current.leftArrowKey.isPressed)
        {
            transform.Rotate(new Vector3(0, 0, 180) * Time.deltaTime);
            childTransform.Rotate(new Vector3(0, 180, 0) * Time.deltaTime);
        }
        if(Keyboard.current != null && Keyboard.current.rightArrowKey.isPressed)
        {
            transform.Rotate(new Vector3(0, 0, -180) * Time.deltaTime);
            childTransform.Rotate(new Vector3(0, -180, 0) * Time.deltaTime);
        }

    }
```

&#x20;추가로 위 코드를 Sphere에 넣어줬다. 이 코드는 위 아래로는 앞, 뒤 움직임을 구현 했고, 양 옆으로는 Sphere의 회전과 Cube가 Sphere 부근에 중심을 놓고 도는 것을 구현했다. 여기서 중요한 점은 Cube가 본인 중심으로 피겨하듯이 도는 게 맞는데 Sphere가 회전하면서 자식인 Cube도 회전하기에 공전하는 것처럼 보이는 것이다. Translate도 진짜 y 값이 1 증가하는게 아닌, 내가 바라보는 방향으로 local하게 y가 1 증가한다. 따라서 다음과 같다.

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

&#x20;코드는 [여기](https://github.com/hoeo159/Unity_Playground/tree/main/Move)에서 볼 수 있는데 일단 고칠 부분이 있다.

* [ ] 레포 최신화 하기
