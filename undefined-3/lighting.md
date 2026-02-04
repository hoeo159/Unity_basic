# Lighting 세부 설정들



<figure><img src="../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

&#x20;설명안했던 부분에 대한 간략한 설명이다.

1. Indirect Resolution : Realtime GI를 계산할 때, 1 unit 당 몇 개의 점(화소)로 계산할 지 정하는 실시간 화질
2. Direct Samples : 태양이나 전등 같은 그림자를 포함한 직접광을 계산할 때 광선을 몇 번 쏠지 정하는 \
   정밀도(노이즈 제거용)를 나타냄
3. Indirect Samples : 간접광을 계산할 때 광선을 몇 번 쏠지 정하는 정밀도(얼룩 제거)
4. Environment Samples : Skybox나 배경에서 오는 환경광을 쏘는 광선 개 수를 정하는 정밀도
5. Max Bounces : 빛이 물체에 부딪혔을 때, 최대 몇 번까지 반사되게 정하는 횟수
6. Lightmap Resolution : 최종적으로 구워질 Lightmap이 1 unit 당 몇 픽셀을 차지할 지 정하는 해상도
7. Albedo boost : 빛이 튕겨내는 성질을 인위적으로 부풀려서 씬 전체를 더 밝게 만드는 설정
8. Indirect Intensity : 다 계산된 간접광의 밝기만 강도를 조절하는 슬라이더
