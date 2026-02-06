# Lightmap

&#x20;게임이나 그래픽스 쪽을 공부하면 **mapping, map**이란 걸 많이 볼 수 있다. 이쪽이 아니더라도 알고리즘 쪽에서 mapping 기법은 무언가에 1 : N으로 대응시키거나 대체하여 시간을 단축시키는 전략을 의미한다. bump map, texture map, normal map, shadow map 등 생각나는 대로 적어 봤는데 그 중에서 이번에는 Lightmap이다. 이것도 다른 map과 비슷하게 물체에 대해 그림자와 조명을 오브젝트에 미리 저장해놓고 필요할 때 look-up table처럼 갖다 쓰겠다는 전략이다.

<div data-full-width="true"><figure><img src="../.gitbook/assets/image (2) (1) (1).png" alt="" width="389"><figcaption></figcaption></figure></div>

<figure><img src="../.gitbook/assets/image (3) (1) (1).png" alt="" width="452"><figcaption></figcaption></figure>

Window - Rendering - Lighting에서 New를 누르면 현재 씬에 대한 새로운 light setting asset을 생성할 수 있다. 그러면 조명 연산을 안하고 그냥 빛이 비춰진 그림 벽을 보게 된다. 하지만 단점이 있다. 맵 이미지 생성으로 용량은 둘째 치고 움직이는 순간 어색해져 버린다. 따라서 **거의 움직이지 않는 물체**에 대해서 적용해줄 필요성이 있다. 또한 씬을 수정할 때마다 Lightmap을 다시 구워줄(bake) 필요가 있다.
