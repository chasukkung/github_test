using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Delivery : MonoBehaviour
{

    [SerializeField] Color32 hasPackageColor = new Color32(1, 1, 1, 1);
    [SerializeField] Color32 noPackageColor = new Color32(0, 0, 0, 0);

    [SerializeField] private float destroyDelay = 0.5f;
    // 클래스 멤버 변수로 올바르게 선언
    private bool hasPackage = false; // 초기값 설정

    SpriteRenderer spriteRenderer;

    private void Start()
    {
        spriteRenderer = GetComponent<SpriteRenderer>();

        // Start 메서드 수정 및 초기 hasPackage 값 로깅
        Debug.Log(hasPackage);
    }

    private void OnCollisionEnter2D(Collision2D other)
    {
        Debug.Log("oops! I did it again");
    }

    // OnTriggerEnter2D 메서드는 Collider2D 파라미터를 사용해야 함
    private void OnTriggerEnter2D(Collider2D other)
    {
        if (other.tag == "Package"&& !hasPackage )
        {
            hasPackage = true; // 패키지를 픽업했다면 true로 설정
            Debug.Log("Package picked up");
            spriteRenderer.color = hasPackageColor;
            Destroy(other.gameObject, destroyDelay);

        }
        else if (other.tag == "customer" && hasPackage)
        {
            hasPackage = false; // 패키지를 고객에게 전달
            Debug.Log("Oh, Thanks that's my package.");
            hasPackage = false;
            spriteRenderer.color = noPackageColor;
        


        }
    }
}
