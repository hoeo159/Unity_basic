# Raycast 기초

&#x20;대부분 게임에서 물리적인 판정을 구분할 때 실제 오브젝트를 이용하여 테스트하기에는 너무 많은 자원이 소모된다. 따라서 가상의 광선을 쐈을 때 다른 Collider와 충돌하는지 검사하는 방식을 Raycast라고 한다. raycast를 실행했을 때 ray가 collider를 가진 오브젝트와 충돌하면 `RaycastHit` 타입의 충돌 정보가 생성된다. 생성된 `RaycastHit` 오브젝트를 통해 충돌한 게임 오브젝트, 충돌 위치, 충돌 위치의 normal vector 등을 알 수 있다.

```
private void Shot() {
    RaycastHit hit;
    Vector3 hitPosition = Vector3.zero;

    // Raycast(시작 지점, 시작 방향, 충돌 정보 컨테이너, 사정거리)
    if(Physics.Raycast(fireTransform.position, fireTransform.forward, out hit, fireDistance))
    {
        IDamageable target = hit.collider.GetComponent<IDamageable>();
        
        if(target != null)
            target.OnDamage(gunData.damage, hit.point, hit.normal);
            
        hitPosition = hit.point;
    }
}
```

&#x20;위 예시 코드를 통해 Raycast의 사용법을 간단하게 볼 수 있다. `Physics.Raycast`를 통해 ray를 쏴서 충돌한 collider가 있는지 parameter 중 `out RaycastHit hitInfo`를 받아서 볼 수 있다. 함수 자체는 충돌에 성공했다면 `true`, 아니면 `false`를 반환한다. `IDamageable`은 이름에서 유추할 수 있다시피 데미지를 받을 수 있는 오브젝트에 대한 interface이다. 만약 아군이나 특정 오브젝트를 무시하려면 LayerMask를 통해 걸러야한다.
