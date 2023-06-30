using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;

public class Hero: MonoBehaviour
{

    float handle_uzanim;
    Vector2 handleVec;
    public Animator animator;

    public FloatingJoystick joystick;
    public Image handle;
    public float rot_speed,move_speed;

    

    void Update()
    {
        Movement();
        Combat();
        
    }
    void Movement()
    {
        
        handleVec = handle.transform.localPosition;
        animator.SetFloat("speed", handle_uzanim);
        float x = joystick.Horizontal;
        float y = joystick.Vertical;
        print(x + "," + y);


        if (x != 0 || y != 0)
        {
            transform.Translate(new Vector3(x, y, 0) * Time.deltaTime * move_speed, Camera.main.transform);
        }

        if (handleVec != Vector2.zero)
        {
            handle_uzanim = Mathf.Sqrt(handleVec.x * handleVec.x + handleVec.y * handleVec.y) / 128;
            float angle = Mathf.Atan2(handleVec.x, handleVec.y) * Mathf.Rad2Deg;
            transform.rotation = Quaternion.Lerp(transform.rotation, Quaternion.Euler(0, -35 + angle, 0), rot_speed * Time.deltaTime);
            
        }
        else
        {
            handle_uzanim -= Time.deltaTime * move_speed ;
            handle_uzanim= Mathf.Clamp(handle_uzanim, 0, 1);
            
        }

        
    }
