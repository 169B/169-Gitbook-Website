---
description: Learn the Programming Basics.
icon: gears
---

# Configuring Your Template

In this specific tutorial we will be using EZ-Template as an example which you downloaded in the previous tutorial. (All new coders should use EZ-Template as a starting point)

{% hint style="info" %}
This specific tutorial is **most helpful** to be used when your robot is **fully built. (Read through it anyway to get a sense of familiarity for the template)**
{% endhint %}

Now we will go through the structure of your files that you should code inside.

{% stepper %}
{% step %}
### Main File Structure

Open the "src" folder on the right.

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

There are two primary files that you will be regularly coding inside:

1. **autons.cpp** - to make your robot perform tasks like move a motor or move forward in a specific direction while in the autonomous period in a match.
2. **main.cpp** - to configure the main characteristics of your robot and create controller functions that move motors or pistons on your bot.
{% endstep %}

{% step %}
### Configuring main.cpp

{% hint style="danger" %}
This is how problems with the robot/code usually arise. **Be careful.**
{% endhint %}

Open the main.cpp c++ file.

You should see:

{% code title="main.cpp (Lines: 9-12)" overflow="wrap" lineNumbers="true" %}
```cpp
ez::Drive chassis(
    {-11, -12, 13}, //Left Motors
    {18, 19, -20}, //Right Motors
    )
```
{% endcode %}

Each number in this Drive Chassis function, eg: -11, refers to a port on a brain[^1] where a drivetrain motor is plugged into:

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

Note the ports the motors are connected to with a cable.

Position the robot so that the front of the robot is in front of you.

Now look at the orientation of the motors:

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

If the orientation of the motors in your drivetrain resembles this, ensure the connected port is positive in the code. **If the VEX logo is flipped, ensure the port number is negative.**

{% code title="main.cpp (Lines: 9-12)" overflow="wrap" %}
```abap
ez::Drive chassis(
    {11, -12}, //Left Ports
    {18, 19}, //Right Ports
    )
```
{% endcode %}

In this example, you can choose how many motors you can select to have, depending on your robot drivetrain.
{% endstep %}

{% step %}
### IMU Setup

{% code title="main.cpp (Lines: 9-12)" overflow="wrap" %}
```abap
ez::Drive chassis(
    {-11, -12, 13},  
    {18, 19, -20}, 

    15,      // IMU Port
```
{% endcode %}

Port 15 denotes the Inertial Measurement Unit (IMU) sensor.

### <mark style="background-color:$danger;">An IMU is required</mark>

The IMU is a sensor that constantly tracks the rotation (heading) of the robot. EZ-Template relies on this heading information to make your autonomous turns and paths accurate and repeatable. **Without an IMU, autonomous turning will be inconsistent, and there is no other built-in way to achieve the same level of accuracy.**

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

Screw this sensor in a place that is flat and not on a moving part, usually flat on a horizontal drivetrain support:

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

When plugged in, change the port in the code.
{% endstep %}

{% step %}
### Drivetrain Setup

{% code fullWidth="true" %}
```abap
    3.25, // Put your Wheel Diameter here
    450) // Put your Wheel RPM = cartridge * (motor gear / wheel gear)
```
{% endcode %}

To finish off your main.cpp Configuration, put your wheel info to help with autonomous movements later.

{% hint style="info" %}
**If your are unsure about anything**, eg. Wheel Diameter/RPM, just ask.
{% endhint %}
{% endstep %}
{% endstepper %}

#### Great Work! :tada::tada:

You have configured all the basics.

Now, as coder you have a choice between Wheel Odometry or using Drivetrain Motor Encoders. These robot tracking methods will assist the robot in moving in accurate and specific ways in the autonomous period.

**Press "Next" to go to the seperate sections to learn how to configure these tracking methods.**

[^1]: A VEX brain is the central control unit of a VEX robotics kit, functioning as the robot's "brain" by running programs, connecting to sensors and motors, and providing real-time feedback through a touch-screen
