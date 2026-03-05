# Tuning PID

PID tuning is how you make autonomous movements **consistent**.

You’ll tune in this order:

1. **Drive** (forward/back)
2. **Turn**

Don’t tune odom until drive + turn feel solid.

***

### Before you tune (2 minute checklist)

* Charge the battery.
* Make sure wheels are tight.
* Make sure drivetrain spins freely.
* Use the same wheel type you compete with.

{% hint style="warning" %}
If the robot slips a lot, PID will look “random”.

Fix slip before changing constants.
{% endhint %}

***

{% stepper %}
{% step %}
### Step 1 — Enable your constants

Open `src/main.cpp`.

Inside `initialize()`, make sure `default_constants();` runs:

{% code title="main.cpp" overflow="wrap" lineNumbers="true" %}
```cpp
void initialize() {
  // ...
  default_constants();
  // ...
}
```
{% endcode %}
{% endstep %}

{% step %}
### Step 2 — Pick one test autonomous

You want a test that is always the same.

Use one of these:

* `drive_example()` to tune drive
* `turn_example()` to tune turns

If you don’t have those, make a tiny tester:

{% code title="autons.cpp" overflow="wrap" lineNumbers="true" %}
```cpp
void pid_test_drive() {
  chassis.pid_drive_set(36_in, 110, true);
  chassis.pid_wait();

  chassis.pid_drive_set(-36_in, 110, true);
  chassis.pid_wait();
}

void pid_test_turn() {
  chassis.pid_turn_set(90_deg, 90);
  chassis.pid_wait();

  chassis.pid_turn_set(0_deg, 90);
  chassis.pid_wait();
}
```
{% endcode %}

{% hint style="info" %}
Tune one thing at a time.

Don’t tune drive and turn in the same run.
{% endhint %}
{% endstep %}

{% step %}
### Step 3 — Find where to change the numbers

Open `src/autons.cpp`.

Find `default_constants()`.

It looks like this:

{% code title="autons.cpp" overflow="wrap" lineNumbers="true" %}
```cpp
void default_constants() {
  // P, I, D
  chassis.pid_drive_constants_set(20.0, 0.0, 100.0);

  // P, I, D, start I
  chassis.pid_turn_constants_set(3.0, 0.0, 20.0, 15.0);
}
```
{% endcode %}

What the values mean:

* `kP` = how hard it pushes toward the target
* `kD` = how hard it slows down near the target
* `kI` = tiny “extra push” at the end (optional)
{% endstep %}

{% step %}
### Step 4 — Tune drive kP (keep kI and kD at 0)

In `default_constants()`:

1. Set drive `kI = 0`.
2. Set drive `kD = 0`.
3. Only change drive `kP`.

Example:

{% code title="autons.cpp" overflow="wrap" lineNumbers="true" %}
```cpp
chassis.pid_drive_constants_set(10.0, 0.0, 0.0);
```
{% endcode %}

Run your drive test.

What you should see:

* Stops short every time → `kP` too low.
* Shoots past a lot → `kP` too high.
* “Bounces” back and forth → `kP` too high.

Increase `kP` until you get **a little bit of overshoot**.

Then stop increasing it.
{% endstep %}

{% step %}
### Step 5 — Tune drive kD (leave kI at 0)

Keep the `kP` you just found.

Now add `kD` until the overshoot mostly goes away.

Example:

{% code title="autons.cpp" overflow="wrap" lineNumbers="true" %}
```cpp
chassis.pid_drive_constants_set(10.0, 0.0, 60.0);
```
{% endcode %}

Good drive movement looks like this:

* Moves fast at the start
* Slows down near the end
* Stops without bouncing
{% endstep %}

{% step %}
### Step 6 — (Optional) Add a tiny bit of drive kI

Only add `kI` if the robot:

* gets close, then never finishes, or
* always stops a little short

Add a very small `kI`.

Then re-check `kD`.

{% hint style="warning" %}
If `kI` is too high, the robot will “creep” or overshoot late.

If that happens, lower `kI` back down.
{% endhint %}
{% endstep %}

{% step %}
### Step 7 — Tune turn PID (same idea)

Now tune turning.

Do the same 2-step loop:

1. Increase turn `kP` until you see a little bounce.
2. Increase turn `kD` until the bounce goes away.

Turn constants have a 4th number.

That 4th number is when `kI` is allowed to start.

Example:

{% code title="autons.cpp" overflow="wrap" lineNumbers="true" %}
```cpp
// P, I, D, start I (degrees)
chassis.pid_turn_constants_set(3.0, 0.0, 20.0, 15.0);
```
{% endcode %}

{% hint style="info" %}
Leave turn `kI = 0` at first.

Only add turn `kI` if it’s always a few degrees off.
{% endhint %}
{% endstep %}

{% step %}
### Step 8 — Lock it in with a “real” mini route

After drive and turn both look good, test this:

1. Drive forward.
2. Turn 90.
3. Drive forward again.

If it’s bad again, your drive and turn constants are not working together yet.

Small changes only.
{% endstep %}
{% endstepper %}

***

### Quick troubleshooting

* One direction is good, the other is bad:
  * Robot is unbalanced or wheels slip differently.
  * Consider separate forward/back constants later.
* Turn is inconsistent:
  * IMU might be loose.
  * IMU might be plugged into the wrong port.
* Everything is “random”:
  * Battery is low.
  * Wheels are slipping.
  * Something is rubbing.
