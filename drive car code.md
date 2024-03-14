using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Driver : MonoBehaviour
{
    [SerializeField] float steerSpeed = 1f;
    [SerializeField] float moveSpeed = 0.01f;

    void Start()
    {
        // 초기화 코드는 필요한 경우에만 여기에 작성합니다.
    }

    void Update()
    {
        float steerAmount = Input.GetAxis("Horizontal") * steerSpeed * Time.deltaTime;
        transform.Rotate(0, 0, -steerAmount);

        float updown = Input.GetAxis("Vertical") * moveSpeed * Time.deltaTime;
        transform.Translate(0, updown, 0);
    }
}
