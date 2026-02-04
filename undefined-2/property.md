# Property

&#x20;사용자의 Input을 관리하는 Player Input에 다음과 같은 코드가 있다.

```
    public float move { get; private set; }
    public float rotate { get; private set; }
    public bool fire { get; private set; }
    public bool reload { get; private set; } 
```

&#x20;이러한 방식을 C#의 property 문법이라고 한다. property는 변숫값을 읽거나 쓰는 과정에서 특별한 처리를 할 수 있는 변수처럼 보이는 메서드이다. property에 새로운 값을 할당할 경우 "set" accessor가 실행되고 가져오는 경우 "get" accessor가 실행된다. 위 코드의 경우에는 읽는 get은 자유롭지만 set을 private로 하여 다른 스크립트에서 바꿀 수 없도록 할 수 있다. 다른 예시를 들어보면

```
public float a = 10.0f;
public float propEg {
    get { return a * 0.0001f; }
    set { a = value * 10.0f; }   
}
// 이후 사용
float myValue = propEg; 
// 1. propEg를 읽으려고 시도함 -> get 발동!
// 2. return a * 0.0001f; 실행
// 3. 10.0 * 0.0001 = 0.001 이 반환됨

Debug.Log(myValue); // 결과: 0.001

propEg = 5.0f;
// 1. propEg에 5.0을 넣으려고 시도함 -> set 발동!
// 2. 여기서 'value'는 5.0f가 됨.
// 3. a = value * 10.0f; 실행
// 4. a = 5.0 * 10.0 -> a는 50.0이 됨.

Debug.Log(a); // 결과: 50.0
```

&#x20;간단하게 쓰는 것과 읽는 방식을 분리할 수 있어서 Read-only 변수처럼 쓸 수 있는 것이다.
