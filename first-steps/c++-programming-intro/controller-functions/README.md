---
icon: gamepad
---

# Controller Functions

Controller functions let you press a **button on the V5 controller** and make a **motor** on your robot move.

On this page you will make **one intake motor** that:

* Spins with buttons during **driver control**
* Can also be used later in **autonomous**

The goal is: **“Press a button → intake moves.”**

***

{% stepper %}
{% step %}
### Step 1 – Find `subsystems.hpp`

1. In your project, open the **`pros`** folder in the file explorer.

<figure><img src="../../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

1. Inside `pros`, look for a file named **`subsystems.hpp`**.
{% endstep %}

{% step %}
### Step 2 – Create the intake motor in `subsystems.hpp`

Open **`pros/subsystems.hpp`** and see something like this inside:

{% code title="subsystems.hpp" overflow="wrap" lineNumbers="true" %}
```cpp
#pragma once

#include "EZ-Template/api.hpp"   // Template header – leave this
#include "api.h"                 // PROS header – leave this

extern Drive chassis;             // Drive object from the template

// Put your motors, sensors, etc. here

inline pros::Motor intake(10);    // Change 10 to the port your intake motor uses
// inline pros::Motor intake(1);
// inline pros::adi::DigitalIn limit_switch('A');
```
{% endcode %}

{% hint style="info" %}
You can name this "intake" Motor anything.

Eg: inline pross::Motor upper\_intake(10);
{% endhint %}

Now edit it for **your robot**:

Look at the orientation of the motor(s):

<figure><img src="../../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

If the orientation of the motors in your drivetrain resembles this, ensure the connected port is positive in the code. **If the VEX logo is flipped, ensure the port number is negative.**

1. Change `10` to the **port** your intake motor is plugged into on the brain.
2. If the intake spins the **wrong way** when you test it later, make the number **negative** (for example, `-10`).

{% hint style="info" %}
#### What does the motor number mean?

`pros::Motor intake(10);`

* `10` is the **port number** on the V5 brain.
* `-10` means **same port**, but tell PROS to **reverse** the motor direction in software.
{% endhint %}

#### Using more than one intake motor (Motor Group)

If your intake has **two or more motors**, you can make a **`MotorGroup`**. A motor group lets you control **several motors as if they were one**:

{% code title="subsystems.hpp – MotorGroup example" overflow="wrap" lineNumbers="true" %}
```cpp
inline pros::MotorGroup intake({10, -11});
// 10  → first intake motor port
// -11 → second intake motor port (reversed)
```
{% endcode %}

* The numbers in `{ ... }` are the **ports** for each intake motor.
* You can still use `-` in front of a port (like `-11`) to **reverse** that motor in software.

Once you use a `MotorGroup` like this, all the code later on this page (`intake.move(127);`, etc.) works **exactly the same** – it will move **all** the motors in the group together.
{% endstep %}

{% step %}
### Step 4 – Make the buttons move the intake (Driver Control)

To move a motor in PROS, you call `move()` with a value between **`-127`** and **`127`**:

```cpp
intake.move(127);   // full speed forward
intake.move(-127);  // full speed backward
intake.move(0);     // stop
```

{% hint style="info" %}
#### What does `-127` to `127` mean?

Think of this number as **power** or **speed**:

* `127` → full speed **forward**
* `0` → **stopped**
* `-127` → full speed **backward**

You can also use values in between, like `60` or `-80`, for slower speeds.
{% endhint %}

Your controller in code is called **`master`**. You can read whether a button is pressed like this:

```cpp
master.get_digital(DIGITAL_L1);  // true if L1 is currently held
```

`DIGITAL_L1` and `DIGITAL_L2` are the **top left shoulder buttons**.

<figure><img src="../../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
**Do Option A or Option B below.**
{% endhint %}

#### Option A – Hold buttons to move the intake (L1 / L2)

In this setup:

* Hold **L1** → intake runs **forward**
* Hold **L2** → intake runs **backward**
* Let go of both → intake **stops**

{% hint style="success" %}
If you would like, **you can** **change the intake buttons to any of the buttons in the above picture: L1, L2, R1, R2, A, B, X, Y, UP, DOWN, LEFT, RIGHT -** by just substituting "DIGITAL\_L1" to "DIGITAL\_R1" or similar in the below code.
{% endhint %}

```cpp
if (master.get_digital(DIGITAL_L1)) {
  intake.move(127);
}
else if (master.get_digital(DIGITAL_L2)) {
  intake.move(-127);
}
else {
  intake.move(0);
}
```

**Put this inside `opcontrol()`**

Open `src/main.cpp` and find the `opcontrol()` function. Replace or edit the existing code so it looks like this:

{% code title="main.cpp – opcontrol() with hold-to-run intake" overflow="wrap" lineNumbers="true" %}
```cpp
void opcontrol() {
  // How your drive behaves when you let go of the joysticks
  chassis.drive_brake_set(MOTOR_BRAKE_COAST);

  while (true) {
    // Extra helper code from the template – just leave this line
    ez_template_extras();

    // Your drive control
    chassis.opcontrol_tank();  // Tank control
    // chassis.opcontrol_arcade_standard(ez::SPLIT);
    // chassis.opcontrol_arcade_standard(ez::SINGLE);
    // chassis.opcontrol_arcade_flipped(ez::SPLIT);
    // chassis.opcontrol_arcade_flipped(ez::SINGLE);

    // Intake control with L1 / L2
    if (master.get_digital(DIGITAL_L1)) {
      intake.move(127);      // intake in
    }
    else if (master.get_digital(DIGITAL_L2)) {
      intake.move(-127);     // intake out
    }
    else {
      intake.move(0);        // stop
    }

    // Small delay so the CPU is not running this loop too fast
    pros::delay(ez::util::DELAY_TIME);
  }
}
```
{% endcode %}

{% hint style="info" %}
#### What is `pros::delay()`?

`pros::delay(number);` **pauses** the program for a short time (the number is in **milliseconds**).

In `opcontrol()`, this:

* Stops the loop from running **too fast**
* Lets timers and other background code work correctly

In short: **always keep this delay at the bottom of the loop.**
{% endhint %}
{% endstep %}
{% endstepper %}



***

### Step 5 – Make a toggle button (press once to start, press again to stop)

Sometimes you don’t want to **hold** a button down. Instead, you can use a **toggle**:

* Press L1 once → intake **turns on** and keeps spinning
* Press L1 again → intake **turns off**

To do this, we use a **boolean** (`bool`).

{% hint style="info" %}
#### What is a boolean (`bool`)?

A `bool` is a variable that can be only **two values**:

* `true` → yes / on
* `false` → no / off

You can think of it like a **light switch**.
{% endhint %}

#### Toggle intake in `opcontrol()`

Here’s an example `opcontrol()` that uses a toggle on **L1**:

{% code title="main.cpp – opcontrol() with toggle intake" overflow="wrap" lineNumbers="true" %}
```cpp
void opcontrol() {
  chassis.drive_brake_set(MOTOR_BRAKE_COAST);

  // Is the intake currently running?
  bool intake_running = false;

  while (true) {
    ez_template_extras();

    chassis.opcontrol_tank();  // Your drive control

    // If L1 was just pressed this moment, flip intake_running
    if (master.get_digital_new_press(DIGITAL_L1)) {
      intake_running = !intake_running;  // true → false, false → true
    }

    // If intake_running is true, spin the intake
    if (intake_running) {
      intake.move(127);
    }
    // If intake_running is false, stop the intake
    else {
      intake.move(0);
    }

    pros::delay(ez::util::DELAY_TIME);
  }
}
```
{% endcode %}

You can choose **either**:

* Hold‑to‑run (L1 / L2)
* Toggle‑to‑run (L1 only)

Use whichever your driver prefers.

***

### Step 6 – (Optional) Use the intake in Autonomous

Because the intake motor is created in `subsystems.hpp`, you can also use it in **autonomous** with the **same `intake.move(...)` calls**.

Below is an example autonomous routine:

* Drive forward **24"**
* Start intaking after **6"** of driving
* Stop the intake when that drive is done
* Turn 45°, then -45°, then back to 0°
* Drive back while **outtaking**, then stop

{% hint style="info" %}
#### Don’t worry if this looks confusing

The `pid_drive_set`, `pid_turn_set`, and similar functions will be explained on the **autonomous pages later**.

For now, just notice **where** `intake.move(127);` and `intake.move(0);` are placed.
{% endhint %}

{% code title="autons.cpp – example intake autonomous" overflow="wrap" lineNumbers="true" %}
```cpp
void intake_autonomous() {
  // Drive forward 24 inches
  chassis.pid_drive_set(24_in, DRIVE_SPEED, true);

  // Wait until we have driven 6 inches, then start the intake
  chassis.pid_wait_until(6_in);
  intake.move(127);                 // start intaking

  // Wait until the drive finishes, then stop the intake
  chassis.pid_wait_quick_chain();
  intake.move(0);                   // stop intake

  // Turn 45 degrees
  chassis.pid_turn_set(45_deg, TURN_SPEED);
  chassis.pid_wait_quick_chain();

  // Turn back -45 degrees
  chassis.pid_turn_set(-45_deg, TURN_SPEED);
  chassis.pid_wait_quick_chain();

  // Turn back to 0 degrees and wait until finished
  chassis.pid_turn_set(0_deg, TURN_SPEED);
  chassis.pid_wait();

  // Drive back 24 inches while outtaking
  intake.move(-127);                // outtake
  chassis.pid_drive_set(-24_in, DRIVE_SPEED, true);
  chassis.pid_speed_max_set(DRIVE_SPEED);
  chassis.pid_wait();
  intake.move(0);                   // stop intake
}
```
{% endcode %}

***

### Quick checklist

If your intake is not working, check:



1. The intake port number in `pros::Motor intake(...)` matches the **brain port**.
2. Your intake code is **inside the `while (true)` loop** in `opcontrol()`.
3. `pros::delay(ez::util::DELAY_TIME);` is still at the **bottom** of that loop.

Once this works, you can repeat the same pattern for **other mechanisms** (arms, claws, wings, etc.) by adding more motors to `subsystems.hpp` and wiring them to controller buttons in `opcontrol()`.

Press next to go to more driver control functions.
