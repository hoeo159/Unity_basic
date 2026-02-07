# Line Renderer

&#x20;Line Renderer는 점(point)과 점 사이를 이어서 선을 그려주는 component이다. 점 몇 개를 찍어서 그 사이를 잇는 굵은 선 or 띠를 화면에 그린다.

&#x20;옛날에 군대에서 경계 근무를 설 때 탄알집이랑 이것저것 챙겨가면 탄알집에 탄두에 붉은 색이 칠해져 있는 것을 볼 수 있었다. 이것은 예광탄으로 보통 5발에 1발, 4 + 1 꼴로 예광탄을 배치하여 어두운 밤에도 탄알이 날아가는 궤적을 볼 수 있도록 하기 위함이었다. 예광탄을 쏘면 붉은 색 line이 남는데 Line Renderer로 이러한 역할을 한다.

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption><p>출처 미합중국 국방부(www.defense.gov)</p></figcaption></figure>

&#x20;게임의 필수 요소는 아니지만 간단한 효과로 게임을 멋있거나 그럴 듯하게 만들 수 있다. 옛날에 코딩 알바할 때도 플랫포머 게임을 만들다가 이걸 알려주니 중딩들이 좋아했다. 저렇게 총알에 line renderer를 할 때에는 두께를 작게하고 총알이 나갈 때 활성화해줘야 하기 때문에 처음에는 비활성화 해줘야 한다. 또한 그림자가 비칠 필요가 없기 때문에 Cast Shadow를 Off해줘야한다.

```
private LineRenderer bulletLineRenderer;
bulletLineRenderer = GetComponent<LineRenderer>();

bulletLineRenderer.positionCount = 2; // 사용할 점을 2개로 변경
bulletLineRenderer.enabled = false;
```

&#x20;위 코드와 같이 init을 할 수 있다. 주로 스크립트 인스턴스가 호출되는 Awake() 메서드에서 사용한다. Awake는 게임 오브젝트가 활성화되자마자 Start 전에 호출되는 메서드이다. Awake가 끝난 후, 첫 번째 Update가 호출되기 전 Start 메서드가 호출된다. 주로 Awake에서 변수를 초기화하고, Start에서 다른 객체를 참조한다.
