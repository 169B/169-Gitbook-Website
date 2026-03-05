---
description: Drive forward, turn, and drive to points using odometry.
---

# Odom Movements (EZ-Template)

Odom movements let you tell the robot **where to go** on the field.

You give it a **target point** like `(x, y)`.

* `x` = right/left (right is positive)
* `y` = forward/back (forward is positive)



{% hint style="info" %}
This page assumes you already set up tracking wheels / odom.

If not, do that first: [Configuring Odometry in C++](../configuring-odometry-in-c++.md)
{% endhint %}

***

### The 3 commands you’ll use most

1. **Set the starting position** (where the robot starts on the field)
2. **Drive to a point**
3. **Wait** for the move to finish

***

{% stepper %}
{% step %}
### Step 1 — Put code in the right place

Open `src/autons.cpp`.

Create a new autonomous function like this:

{% code title="autons.cpp" overflow="wrap" lineNumbers="true" %}
```cpp
void odom_test_auto() {
  // odom moves go here
}
```
{% endcode %}

{% hint style="info" %}
Keep one route per function.

Name it after the route, not the season.
{% endhint %}
{% endstep %}

{% step %}
### Step 2 — Set your starting position

At the start of the autonomous function, set where the robot begins.

Most of the time you start at `(0, 0)` facing `0°`.

{% code title="autons.cpp" overflow="wrap" lineNumbers="true" %}
```cpp
void odom_test_auto() {
  // Start at the origin, facing "forward"
  chassis.odom_xyt_set(0_in, 0_in, 0_deg);

  // Your moves go next...
}
```
{% endcode %}

{% hint style="warning" %}
If your robot starts in a different place on the field, change these numbers.

If you don’t set this, the robot’s idea of its position may be wrong.
{% endhint %}
{% endstep %}

{% step %}
### Step 3 — Drive forward (simple example)

This drives to the point `(0, 24)`.

That means **24 inches forward**.

{% code title="autons.cpp" overflow="wrap" lineNumbers="true" %}
```cpp
void odom_test_auto() {
  chassis.odom_xyt_set(0_in, 0_in, 0_deg);

  // Go to (x=0, y=24) going forward
  chassis.pid_odom_set({{0_in, 24_in}, fwd, 110});
  chassis.pid_wait();
}
```
{% endcode %}

What the inputs mean:

* `{0_in, 24_in}` = the target point `(x, y)`
* `fwd` = drive there **forward**
* `110` = speed limit (0–127)
{% endstep %}

{% step %}
### Step 4 — Drive backward (simple example)

Sometimes you want the robot to drive to a point **while facing backward**.

{% code title="autons.cpp" overflow="wrap" lineNumbers="true" %}
```cpp
void odom_test_auto() {
  chassis.odom_xyt_set(0_in, 0_in, 0_deg);

  // Go to (0, 24) but drive there backward
  chassis.pid_odom_set({{0_in, 24_in}, rev, 110});
  chassis.pid_wait();
}
```
{% endcode %}

{% hint style="info" %}
`rev` does not mean negative inches.

It means “drive in reverse to reach the point”.
{% endhint %}
{% endstep %}

{% step %}
### Step 5 — Turn to face a point

This turns in place to face the point `(24, 24)`.

{% code title="autons.cpp" overflow="wrap" lineNumbers="true" %}
```cpp
void odom_test_auto() {
  chassis.odom_xyt_set(0_in, 0_in, 0_deg);

  // Turn to face (24, 24)
  chassis.pid_turn_set({24_in, 24_in}, fwd, 90);
  chassis.pid_wait();
}
```
{% endcode %}

What the inputs mean:

* `{24_in, 24_in}` = the point you want to face
* `fwd` = face it with the robot’s **front**
* `90` = speed limit
{% endstep %}

{% step %}
### Step 6 — Drive to a point, then do a mechanism action mid‑drive

Use `pid_wait_until(...)` to trigger an action partway through.

Example:

* Drive to `(0, 36)`
* Start the intake after `12"`
* Stop the intake after the drive ends

{% code title="autons.cpp" overflow="wrap" lineNumbers="true" %}
```cpp
void odom_intake_example() {
  chassis.odom_xyt_set(0_in, 0_in, 0_deg);

  chassis.pid_odom_set({{0_in, 36_in}, fwd, 110});

  // After 12 inches of progress, start the intake
  chassis.pid_wait_until(12_in);
  intake.move(127);

  // Wait for the move to finish
  chassis.pid_wait();
  intake.move(0);
}
```
{% endcode %}

{% hint style="info" %}
This only works if `intake` is defined in `include/subsystems.hpp`.

That is covered on [Controller Functions](../controller-functions/).
{% endhint %}
{% endstep %}

{% step %}
### Step 7 — A complete “first real route” example

This is a good first route to test odom:

1. Drive forward 24 inches.
2. Turn to face the right.
3. Drive to a diagonal point.
4. Drive back to the start.

{% code title="autons.cpp" overflow="wrap" lineNumbers="true" %}
```cpp
void first_odom_route() {
  chassis.odom_xyt_set(0_in, 0_in, 0_deg);

  // 1) forward
  chassis.pid_odom_set({{0_in, 24_in}, fwd, 110});
  chassis.pid_wait();

  // 2) face right (turn to look at a point to the right)
  chassis.pid_turn_set({24_in, 0_in}, fwd, 90);
  chassis.pid_wait();

  // 3) drive to a diagonal point
  chassis.pid_odom_set({{24_in, 24_in}, fwd, 110});
  chassis.pid_wait();

  // 4) go back home
  chassis.pid_odom_set({{0_in, 0_in}, rev, 110});
  chassis.pid_wait();
}
```
{% endcode %}
{% endstep %}
{% endstepper %}

***

### Quick fixes if it “drives weird”

* Robot goes the wrong direction:
  * Check tracking wheel ports and directions.
  * Re-check your odom setup: [Configuring Odometry in C++](../configuring-odometry-in-c++.md)
* Robot starts fine, then drifts:
  * Check tracking wheel tension.
  * Make sure wheels are not slipping.
* Robot is correct, but the route is mirrored:
  * Your coordinate signs are flipped.
  * Try changing `x` to `-x` in your target points.

***

### What to do next

1. Make a route sketch with 3–5 checkpoints.
2. Turn each checkpoint into one `pid_odom_set(...)`.
3. Test it 10 times.
4. Only then add mechanisms.
