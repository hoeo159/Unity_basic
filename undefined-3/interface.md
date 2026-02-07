# interface

### interface에 관하여

&#x20;일반적으로 플레이어는 게임 오브젝트에 속하고 좀비, 상자, 벽 등 역시 오브젝트에 속한다. 이러한 오브젝트들은 타입에 따라 상호작용이 서로 다르다. 예를 들어 몬스터는 체력을 깎고, 상자는 부서지고 아이템 생성, 벽은 총알이 박히는 역할을 하게 될 것이다. 이런 것들은 물론 if문을 여럿 사용하여 구현 할 수 있지만 interface를 이용하면 보다 효과적으로 이러한 상호작용들을 구현할 수 있다.

&#x20;interface는 외부와 통신하는 공개적인 통로, 규칙, 기준을 말한다. 하지만 이러한 규격을 만족시킨다면 내부 통로에는 어떤 일이 일어나는 지는 관여하지 않는다. C# interface는 어떤 메서드를 구현하도록 강제하는 제약을 만들 수 있다.

```
public interface I_Item
{
    void Use(GameObject target);
}
```

&#x20;I\_Item의 Use() 메서드는 아이템을 사용하는 메서드이다. 사용할 대상은 target으로 GameObject 타입으로 입력받는다. interface의 메서드는 이렇게 선언만 하고 구현은 없다. 메서드의 형태만 결정하고 자신을 상속하는 클래스에 구현을 맡긴다. 때문에 상속한 클래스는 이 메서드를 반드시 public으로 선언해야한다.

```
public class AmmoPack : MonoBehaviour, I_Item {
    public int ammo = 30; // 충전할 총알 수

    public void Use(GameObject target) {
        Debug.Log("탄알 : " + ammo);
    }
}

public class HealthPack : MonoBehaviour, I_Item {
    public float health = 50; // 체력을 회복할 수치

    public void Use(GameObject target) {
        Debug.Log("체력 회복 : " + health);
    }
}
```

&#x20;I\_Item을 상속한 클래스는 반드시 Use() 메서드를 구현해야 한다.

### 느슨한 커플링

&#x20;만약 어떤 스크립트에서 I\_Item 인터페이스를 상속한 클래스로부터 생성된 오브젝트에 접근했다고 가정해보자. 이 클래스는 Use() 메서드가 구현되어있음이 보장된다. 따라서 오브젝트가 I\_Item 타입으로 취급이 된다면 구체적으로 타입을 검사하지 않고 Use() 메서드를 실행할 수 있다.  Use를 쓰는 클래스를 예시로 들어보자.

```
void OnTriggerEnter(Collider other)
{
    I_Item item = other.GetComponent<I_Item>();
    if(item != null)
    {
        item.Use();
    }
}
```

&#x20;item의 타입은 현재 2번 째 예시 코드에서 알 수 있듯이 AmmoPack과 HealthPack 중 하나이다. 하지만 구체적인 타입을 명시하거나 if로 분기하지 않아도 Use를 우선 시행할 수 있게 해준다. 이러한 특징을 느슨한 커플링이라고 한다. 다시 처음으로 돌아가 플레이어가 어떤 오브젝트를 쐈다면,

```
public interface I_Damage
{
    void onDamage(float damage, Vector3 hitPoint, Vector3, hitNormal)
}
```

&#x20;맞은 오브젝트가 몬스터인지, 벽인지, 상자인지 구체적으로 검사하지 않아도 된다. 함수의 일반적인 type override의 class에  따른 object type 버전인 것 같기도 하고??
