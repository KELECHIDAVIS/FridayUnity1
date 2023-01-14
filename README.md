using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerCam : MonoBehaviour
{
    public float sensX;
    public float sensY;

    public Transform orientation;
    float xRotation; 
    float yRotation; 
    
    private void Start()
    {
        Cursor.lockState = CursorLockMode.Locked;
        Cursor.visible = false; 

    }
    private void Update()
    {
        // get mouse input 
        float mouseX = Input.GetAxisRaw("Mouse X") * Time.deltaTime * sensX; 
        float mouseY = Input.GetAxisRaw("Mouse Y") * Time.deltaTime * sensY;
        // sounds confusing but this is just how unity does it 
        yRotation += mouseX;

        xRotation -= mouseY;
        Mathf.Clamp(xRotation, -90f, 90f);

        //rotate cam and orientation
        transform.rotation = Quaternion.Euler(xRotation, yRotation, 0); // rotate camera 
        orientation.rotation = Quaternion.Euler(0, yRotation, 0); //  rotate player 
    }
}
