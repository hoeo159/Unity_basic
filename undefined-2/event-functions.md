# Event Functions

&#x20;Monobehaviour을 이용한 C# 스크립트를 만들 때 항상 Start()와 Update() 함수가 존재한다. 특정 타이밍이나 시점에 자동으로 호출해주기 위한 메서드들이 많은데 이런 것들을 event function, lifecycle method라고 불린다.

#### Update 계열

1. FixedUpdate()
   1. 고정된 시간 간격(0.02초)마다 호출, 프레임 속도(FPS)와 상관없이 일정하게 실행
   2. 주로 물리 연산(Rigidbody 이동이나 Addforce 등)에 사용된다. 터널링 현상 방지
   3. Time.deltaTime = 0.02s (설정값 유지, 고정)
2. Update()
   1. 매 프레임마다 한 번씩 호출(컴퓨터 성능에 따라 달라짐)
   2. 대부분의 로직, 키 입력 등 처리
   3. Time.deltaTime = 지난 프레임에서 걸린 시간(성능에 따라 다름 60FPS가 약 0.0167s)
3. LateUpdate()
   1. 모든 Update가 끝난 직후에 호출
   2. 카메라 이동에 주로 쓰인다
   3. 만약 캐릭터 움직임과 카메라가 Update에 같이 움직일 때 운이 안 좋으면 카메라가 떨림(Jitter)

#### State 계열

1. OnEnable()
   1. 오브젝트나 스크립트가 활성화될 때마다 호출(Awake 직후 or 꺼졌다가 켜질 때)
   2. 이벤트 연결, 초기 상태 리셋
2. OnDisable
   1. 오브젝트나 스크립트가 비활성화 될 때
   2. 이벤트 연결 해제, [coroutine](../undefined-3/coroutine.md) 중지
3. OnDestroy()
   1. 오브젝트가 완전히 파괴되기 직전에 호출
   2. 메모리 정리, 생성했던 material 삭제 등 정리 작업

#### 물리 충돌 감지

1. OnCollisionEnter(Collison other) / Stay / Exit
   1. 물리적인 충돌이 일어났을 때
2. OnTriggerEnter(Collider other) / Stay / Exit
   1. [물체를 통과할 때](../undefined-1/is-trigger.md)

#### Editor 및 Debugging

1. OnDrawGizmos()
   1. 씬 뷰에 보이지 않는 범위, 경로, 아이콘 등을 선이나 도형으로 그려서 디버
2. OnValidate()
   1. Inspector 창에서 값을 수정할 때마다 호출, 데이터의 무결성 검사나 실시간 반영에 쓰인다



&#x20;정리해보면 대표적으로 일어나는 Eventfunction은 \
Awake(초기화) > OnEnable(이벤트 등록) > Start(타 객체 참조) > Update(로직) > FixedUpdate(물리) > OnDisable(이벤트 해제) 순서가 되겠다\~
