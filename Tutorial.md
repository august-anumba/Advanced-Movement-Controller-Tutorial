# Vertical Movement Controller Tutorial

This tutorial shows how to create a advanced movement controller like sprinting and crouching in Unity.

## 1. Adding and adjusting the `PlayerMovement` C# Script

Firstly we private `float moveSpeed` and create two new public floats, `float walkSpeed`, and `float sprintSpeed` and from now on we change the two new floats in unity and `moveSpeed` will be changed inside of the script;

```.cs
    private float moveSpeed;
    public float walkSpeed;
    public float sprintSpeed;
```

We also need to add Keybind/KeyCodes to control our new advanced movements like sprinting and crouching:

```.cs
    public KeyCode sprintKey = KeyCode.LeftShift;
    public KeyCode crouchKey = KeyCode.LeftControl;
```









```.cs

```
