---
description: Learn the Programming Basics.
icon: steering-wheel
---

# Driver Controls

Driver controls decide how your robot _feels_ to drive in a competition. On this page you'll learn how to tune:

* Control schemes (tank vs arcade)
* Joystick curves
* Active brake

All of these are **driver preferences**. Try them, tweak them, and keep what you like.

{% stepper %}
{% step %}
### Finding `main.cpp`

In your project, open the `src` folder in the file explorer.

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### Control Schemes

There are multiple ways to map the **joysticks** (the two sticks on your V5 controller) to your drive. The drive code supports:

* **Tank drive**
* **Arcade drive** (split and single-stick, standard and flipped)

Pick the one your driver likes best by **uncommenting** the corresponding line in `opcontrol()`.

#### Example `opcontrol()` setup

```cpp
void opcontrol() {
  // ...
  while (true) {
    // ...

    chassis.opcontrol_tank();                        // Tank control
    // chassis.opcontrol_arcade_standard(ez::SPLIT);  // Standard split arcade
    // chassis.opcontrol_arcade_standard(ez::SINGLE); // Standard single-stick arcade
    // chassis.opcontrol_arcade_flipped(ez::SPLIT);   // Flipped split arcade
    // chassis.opcontrol_arcade_flipped(ez::SINGLE);  // Flipped single-stick arcade

    // ...
    pros::delay(ez::util::DELAY_TIME);  // Used for timer calculations. Keep ez::util::DELAY_TIME
  }
}
```
{% endstep %}
{% endstepper %}

***

#### Tank drive

Tank drive lets you control **each side** of the drive separately:

* Left stick → left side of the drive
* Right stick → right side of the drive

This is the **default** control mode in the example project.

```cpp
chassis.opcontrol_tank();
```

<img src="../../.gitbook/assets/file.excalidraw (2).svg" alt="" class="gitbook-drawing">

***

#### Arcade drive

Arcade drive gives you control over:

* **Forward / reverse**
* **Turning**

There are two main flavors: **split arcade** and **single-stick arcade**.

**Split arcade**

In split arcade, one joystick controls forward/backward, and the other controls turning.

* **Standard split arcade**: left stick = forward/reverse, right stick = turn
* **Flipped split arcade**: right stick = forward/reverse, left stick = turn

{% tabs %}
{% tab title="Standard" %}
```cpp
// Standard split arcade
chassis.opcontrol_arcade_standard(ez::SPLIT);
```
{% endtab %}

{% tab title="Flipped" %}
```cpp
// Flipped split arcade
chassis.opcontrol_arcade_flipped(ez::SPLIT);
```
{% endtab %}
{% endtabs %}

<img src="../../.gitbook/assets/file.excalidraw (3).svg" alt="" class="gitbook-drawing">

**Single-stick arcade**

In single-stick arcade, **one joystick** controls _both_ forward/backward and turning.

* **Standard single-stick arcade**: left stick does fwd/rev + turn
* **Flipped single-stick arcade**: right stick does fwd/rev + turn

{% tabs %}
{% tab title="Standard" %}
```cpp
// Standard single-stick arcade
chassis.opcontrol_arcade_standard(ez::SINGLE);
```
{% endtab %}

{% tab title="Flipped" %}
```cpp
// Flipped single-stick arcade
chassis.opcontrol_arcade_flipped(ez::SINGLE);
```
{% endtab %}
{% endtabs %}

<img src="../../.gitbook/assets/file.excalidraw (4).svg" alt="" class="gitbook-drawing">

***

### Joystick Curves

#### Why use joystick curves?

Normally, moving the joystick halfway sends about **50% power** to the motors, where **power** means how hard the motors are being driven relative to their maximum (for example, `50% power` ≈ half speed, `100% power` ≈ full speed).

With an input curve, pushing the joystick halfway might only send **25% power**.

This gives you:

* Finer control at **low speeds** (for lining up shots, intakes, etc.)
* Less "twitchy" behavior around the center of the stick

Some drivers love curves, some hate them. Many newer drivers like stronger curves; experienced drivers often reduce or turn them off. You can **tune these curve values in code** so you can experiment between practice runs.

#### What curve is used?

This code uses the joystick curve that team 5225A used during _In the Zone_.

* **x-axis**: joystick input
* **y-axis**: motor output (power)

You don't need the exact equation to use it—just know that **higher curve values** make the drive more sensitive at low speeds and less sensitive near full stick.

***

#### Setting your joystick curve in code

Once you find curve values you like, keep them by **setting them directly in `main.cpp`**.

In `main.cpp`, inside `initialize()`, you'll find:

```cpp
void initialize() {
  // ...
  chassis.opcontrol_curve_default_set(2.1);
  // ...
}
```

This function sets the **default curve value** for your drive.

* For tank: this value applies to both sides
* For arcade: this follows the same mapping as above (left/right vs fwd/turn, depending on mode)

Change `2.1` to whichever curve value you like.

***

### Active Brake

By default, the drive runs on **coast**: when you let go of the joysticks, the motors stop actively driving but the wheels can **roll freely**, so the robot slowly coasts to a stop.

Many teams prefer this, and some don't like the feel of normal `brake` or `hold`. Active brake gives you something in between.

Enable active brake in `initialize()`:

```cpp
void initialize() {
  // ...
  chassis.opcontrol_drive_activebrake_set(2.0);  // Sets active brake kP (how strong the P loop is). ~2 is a good starting point. 0 disables it.
  // ...
}
```

Try small changes (e.g. `1.0`, `2.0`, `3.0`) and see how quickly the robot stops when you release the stick. M**ost drivers just run coast, eg. (0.0).**

***

You now have full control over how your robot feels to drive:

* Choose a **control scheme** that fits your driver.
* Tune **curves** for precision.
* Use **active brake** to control how fast you stop.

Once your driver is comfortable, you’re ready to move on to more advanced autonomous and driver-assist features.
