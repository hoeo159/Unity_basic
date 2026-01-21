# frame과 실제 시간 다루기

&#x20;게임 개발 외에도 그래픽스 수업 등 화면에 보여지는 것을 다루는 것이라면 사용자마다 시간마다 지나가는 frame이 다르다는 것을 누구나 알 수 있다. 옛날에 콘솔이 주 시장이었을 때는 사양이 비슷해서 frame으로 다루기가 수월했지만 요즘은 개인 pc에 따라 성능이 천차만별이기 때문에 성능에 따라 게임의 난이도가 달라지면 매우 곤란하다.

&#x20;하지만 우리의 MonoBehavior는 기본적으로 `Start()`와 `Update()`만이 있고 이는 frame 별 행동을 정의하지 단위 timestamp를 다루지 않는다. 따라서 우리는 이전 frame과 현재 frame 간 시간을 재야할 필요성이 있다. `Time.deltaTime`은 이러한 시간 차이를 제공해주는 매서드이다.

```
Update()
{
    spawnAfter += Time.deltaTime;
    if spawnAfter >= spawnRate
        spawnAfter = 0;
        // spawnRate(초)마다 하는 행동들~~
}
```

&#x20;요런 식으로 쓸 수 있다. 대개 많이 prefabs을 복제하는게

```
Instantiate(원본 prefab, 생성 위치, 생성 회전);
```

&#x20;물론 Instantiate와 Destroy를 자주 사용하면 성능이 떨어진다. 메모리 가비지가 생기기 때문에 100개를 미리 만들고 on/off 해서 재활용하겠다\~는 패러다임이 오브젝트 풀링(Object Pooling)이다.
