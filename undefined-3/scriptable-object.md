# Scriptable Object

&#x20;게임에는 여러가지 총 또는 총알이 존재한다. 만약 Gun 스크립트에 Gun의 모든 데이터가 변수로 선언되어 있으면 여러가지 문제가 생긴다.

* 총의 수치 데이터만 따로 관리하기 힘들다
* 같은 수치를 가진 타입의 총들이 데이터를 각자 가지게 된다
* 게임 도중에 총의 외형은 가만히 두고 데이터만 교체하기 힘들다

&#x20;따라서 유니티 프로젝트의 에셋형태로 데이터를 담을 수 있는 Scriptable Object가 필요하다. 말 그대로 Object인데 Script로 되어 있는 것이다. 예시로 좀 더 이해해 본다면

```
public class Gun : MonoBehaviour {
    public AudioClip shotClip // 발사 소리
    public AudioClip reloadClip // 재장전 소리
    
    public float damage = 25;
    public int magCapacity = 30;
    
    public float timeBetFire = 0.12f;
    public float reloadTime = 1.8f;
    // etc...
}
```

&#x20;일단 이렇게 만들고 나중에 프로젝트를 확장하여 다양한 총을 구현한다면 위 변수들은 총마다 다른 값들을 가지게 될 것이다. 근데 이 수치들은 Gun 컴포넌트(스크립토 또는 인스턴스)에 종속되어 있다. 만약 게임에 총이 100개 생성된다면, 똑같은 데미지 수치 데이터도 100번 중복되어 메모리에 올라가는 비효율이 발생한다. 따라서 데이터만 따로 관리할 수 있는 저장소가 필요한데, 이때 Scriptable Object를 사용한다. 즉 Gun과 GunData를 분리하는 것이다. Scriptable Object는 다음과 같은 특징을 가진다.

* GunData 오브젝트가 유니티 에디터에서 편집할 수 있는 형태로 존재
* 씬 위의 게임 오브젝트가 아닌 형태로 존재(씬 밖에서도 편집할 수 있도록)
* 여러 오브젝트가 사용할 수 있도록 asset 형태로 저장

&#x20;Scriptable Object를 만들기 위해 클래스에 다음과 같은 코드를 추가한다.

```
[CreateAssetMenu(menuName = "Scriptable/GunData", fileName = "Gun Data")]
public class GunData : ScriptableObject
```

&#x20;위 방식을 통해 project 탭에서 Scriptable이 추가되어 있는 것을 볼 수 있다.

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption><p>project - + - Scriptable</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption><p>asset 생성 및 parameter 할당</p></figcaption></figure>
