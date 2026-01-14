# 간단한 playerController

```
using UnityEngine;
using UnityEngine.InputSystem;

public class PlayerController : MonoBehaviour
{
    private Rigidbody playerRigidbody;
    public float speed = 8.0f;
    public float jumpForce = 5.0f;
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        if (playerRigidbody == null)
        {
            playerRigidbody = GetComponent<Rigidbody>();
        }
    }

    // Update is called once per frame
    void Update()
    {
        if (Keyboard.current == null) return;

        float xVec = 0.0f;
        float zVec = 0.0f;

        if (Keyboard.current.wKey.isPressed) zVec += 1.0f;
        if (Keyboard.current.sKey.isPressed) zVec -= 1.0f;
        if (Keyboard.current.aKey.isPressed) xVec -= 1.0f;
        if (Keyboard.current.dKey.isPressed) xVec += 1.0f;

        Vector3 moveDir = new Vector3(xVec, 0.0f, zVec).normalized;

        playerRigidbody.linearVelocity = new Vector3(moveDir.x * speed, playerRigidbody.linearVelocity.y, moveDir.z * speed);

        if(Keyboard.current.spaceKey.wasPressedThisFrame)
        {
            if(Mathf.Abs(playerRigidbody.linearVelocity.y) < 0.01f)
            {
                playerRigidbody.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
            }
        }
    }

    public void Die()
    {
        gameObject.SetActive(false);
    }
}

```

땅에 붙어 있는 isGrounded() 함수를 만들기 귀찮아서 저렇게 했는데 뭔가 디테일한 isGrounded 함수가 있나???

움직일 때 linearVelocity 말고 AddForce로 해도 움직임을 느낄 수 있다. ForceMode 중 디폴트인 Force로 그냥 놓고 하면 캐릭터의 무게감??을 몬가 느낄 수 있다. 닷지는 사실 점프는 필요 없는데 만들어보고 싶어서 만들었다.
