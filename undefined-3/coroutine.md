# Coroutine

&#x20;[Line Renderder](../undefined-2/line-renderer.md)로 탄알 궤적을 그릴 때 탄알에 대해 발사 효과를 재생하는 메서드를 완성해야한다. 이를 위해서는 Line Renderer Component를 켜서 선을 그린 다음 Line Renderer를 다시 꺼야 한다. 이떄 매우 짧은 시간 동안 처리를 일시 정지한다. 따라서 끄고 켜는 처리 사이에 대기 시간이 필요한 데 이때 코루틴(Coroutine)이 사용된다.

&#x20;Coroutine 메서드는 대기 시간을 가질 수 있는 메서드이다. `IEnumerator` 타입을 반환해야 하며, 처리가 일시 대기할 곳에 `yield` 키워드를 명시해야 한다. 예를 들어

```
void TodayWork(){
    // 밥 먹기
    // 똥 싸기
    // 잠 자기
}
```

&#x20;일반적인 메서드는 `TodayWork`를 부르면 일과를 연속적으로 실행한다. 하지만

```
IEnumerator TodayWork(){
    // 밥 먹기
    yield return new WaitForSecond(10f); // 10초 동안 쉬기
    // 똥 싸기
    yield return null; // 1 프레임만 쉬기
    // 잠 자기
}

// 실행 방법
StartCoroutine(TodayWork());
StartCoroutine("TodayWork");
// 문자열 입력 시, 도중에 종료 가능
StopCoroutine("TodayWork");
// 리턴 값을 즉시 StartCoroutine에 넣어주는 방식은 다음과 같이 입력 값을 전달 가능
StartCoroutine(TodayWork(100));
```

&#x20;이후 코루틴 메서드는 `StartCoroutine(TodayWork());` 또는 이름으로 실행한다. yield 문을 만나면 코루틴 진행이 일시 정지된다. 코루틴이 쉬는 동안 프로그램의 다른 코드가 실행될 수 있다. 대기시간이 끝나면 프로그램의 처리가 코루틴의 마지막 실행 줄로 되돌아 간다. 그리고 남은 처리를 이어서 진행한다.
