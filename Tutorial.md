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

To create these states we use a `public enum` called `MovementState`. Inside this newly create enum we define the different states like walking, sprinting and air and crouching. We will also create a sperate `MovementState` variable called `state` and this will always store the current state of the player is in.
The code should look like this:

```.cs
public MovementState state;
    public enum MovementState
    {
        walking,
        sprinting,
        crouching,
        air
    }
```

We now need to create a new function called `StateHandler` and inside it add some if statements to handle the players state at different times as its name suggests. For example if the player is `grounded` and pressing the `sprintKey` we are going to want to set the players `MovementState` to `sprinting` and set the `moveSpeed` to `sprintSpeed`. We repeat if statements like this for all states the player can be in:

```.cs
private void StateHandler()
    {
        // Mode - Crouching
        if (Input.GetKey(crouchKey))
        {
            state = MovementState.crouching;
            moveSpeed = crouchSpeed;
        }

        // Mode - Sprinting
        else if(grounded && Input.GetKey(sprintKey))
        {
            state = MovementState.sprinting;
            moveSpeed = sprintSpeed;
        }

        // Mode - Walking
        else if (grounded)
        {
            state = MovementState.walking;
            moveSpeed = walkSpeed;
        }

        // Mode - Air
        else
        {
            state = MovementState.air;
        }
    }
```

After this all that is left to do is call this function in `private void Update()` and back in unity we assign values to the variables like Walk Speed, Sprint Speed.

![image](https://github.com/august-anumba/Advanced-Movement-Controller-Tutorial/assets/146851823/91197d4d-b9c1-48c6-a960-767643d44aa3)

However you will notice that crouching doesn't work yet as we havent set up the movements and actions for it.

Back in the `PlayerMovement` script we add a new header and 2 new `public float`'s for `crouchSpeed`, `crouchYScale`, and a `private float startYScale`

```.cs
    [Header("Crouching")]
    public float crouchSpeed;
    public float crouchYScale;
    private float startYScale;
```

We have already implimented the crouchKey Keycode as well as the implimenting it into the if statements in the function `StateHandler`. All that is left to do is make the backbone of it. This begins with saving the normal y scale of the player to `startYScale` variable in `private void Start()` with:

```.cs
        startYScale = transform.localScale.y;
```

We can now go into the `MyInput` function that was created earlier and perform a check if the player has pressed down the crouch key which we have binded to the left ctrl key, and if the player has pressed down the key we want to shrink the player down by setting the local scale to a new `Vector3`, keeping the x and z scale the same and changing the y scale to the `crouchYScale` variable.

```.cs
        if (Input.GetKeyDown(crouchKey))
        {
            transform.localScale = new Vector3(transform.localScale.x, crouchYScale, transform.localScale.z);
        }
```

However doing this we run into a problem, by shrinking the player scale we effectivly leave them smaller and floating in the air. To fix this we simply apply some force downwards when shrinking the player to push them back to the ground:

![image](https://github.com/august-anumba/Advanced-Movement-Controller-Tutorial/assets/146851823/53b12e95-c74e-48c9-8ae8-bc70fbf21406)

We do this by using:

```.cs
            rb.AddForce(Vector3.down * 5f, ForceMode.Impulse);
```

To now stop crouching the player will need to release the crouch key which it currently set to left ctrl, so we run a command to check if the crouch key was realeased yet and set the player scale back to  normal if it has been released.

```.cs
        if (Input.GetKeyUp(crouchKey))
        {
            transform.localScale = new Vector3(transform.localScale.x, startYScale, transform.localScale.z);
        }
```

However we want the player to be slowed while crouching
