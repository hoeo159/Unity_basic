# Coroutine을 이용한 Effect 구현(Code)

```
public class Gun : MonoBehaviour {
    public ParticleSystem muzzleFlashEffect; // 총구 화염 효과
    public ParticleSystem shellEjectEffect; // 탄피 배출 효과

    private LineRenderer bulletLineRenderer; // 탄알 궤적을 그리기 위한 렌더러

    private AudioSource gunAudioPlayer; // 총 소리 재생기
    // 생략....

    // 발사 이펙트와 소리를 재생하고 탄알 궤적을 그림
    private IEnumerator ShotEffect(Vector3 hitPosition) {
        muzzleFlashEffect.Play(); // 총구 화염 효과 재생
        shellEjectEffect.Play(); // 탄피 배출 효과 재생

        gunAudioPlayer.PlayOneShot(gunData.shotClip); // 발사 소리 재생

        bulletLineRenderer.SetPosition(0, fireTransform.position); // 라인 렌더러의 시작 위치 설정
        bulletLineRenderer.SetPosition(1, hitPosition); // 선의 끝점은 입력으로 들어온 충돌 위치
        bulletLineRenderer.enabled = true;
        
        // 0.03초 동안 잠시 처리를 대기
        yield return new WaitForSeconds(0.03f);

        // 라인 렌더러를 비활성화하여 탄알 궤적을 지움
        bulletLineRenderer.enabled = false;
    }
}
```

* Gun 오브젝트에 파티클 시스템 컴포넌트 효과는 Play 메서드로 재생
* 오디오 클립 컴포넌트 효과는 PlayOneShot() 메서
  * Play 메서드는 이미 재생 중인 오디오가 있다면 정지하고 처음부터 재생
  * 연달아 재생되는 총 연사음에는 맞지 않음(소리 중첩 X)
* LineRenderer는 Coroutine을 이용하여 설계

