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
To effectivly allow the player to transition from walking, sprinting, crouching as well as being in the air, it is simpler to manage it using movement states for the character for each state they could be in:

![image](https://github.com/august-anumba/Advanced-Movement-Controller-Tutorial/assets/146851823/049a5e4e-ed69-4e84-99a4-1406c9868c62)

To create these states we use a `public enum` called `MovementState`. Inside this newly create enum we We use the following code to program this

```.cs

```








```.cs

```
