---
description: Learn the Programming Basics.
icon: terminal
---

# Tracking Systems

Now, as coder you have a choice between Wheel Odometry or using Drivetrain Motor Encoders. These robot tracking methods will assist the robot in moving in very accurate and specific ways in the autonomous period.



{% columns %}
{% column width="50%" %}
## Wheel Odometry



This type of tracking specifically uses a rotation sensor that is attached to a seperate wheel, away from the Drivetrain.

These wheels freely roll along the field surface and provide extremely accurate positional feedback.

There are two main types of wheel odometry systems:

1. **One-Wheel Odometry (Vertical)**
   * **Measures just forward/backward.**
2. **Two-Wheel Odometry (Vertical and Horizontal)**
   * **Measures forward/backward and sideways movement.**

{% hint style="danger" %}
<mark style="color:red;">If your robot is using all omni-wheels (no traction wheels),</mark> <mark style="color:red;"></mark><mark style="color:red;">**it is highly recommended to use Two-Wheel Odometry**</mark> <mark style="color:red;"></mark><mark style="color:red;">as more wheel slip will be introduced.</mark>
{% endhint %}

<div data-with-frame="true"><figure><img src="../../.gitbook/assets/Screenshot 2025-12-03 at 12.04.02 am.png" alt=""><figcaption><p>Here you can see both the Horizontal and Vertical Odometry Wheel Trackers.</p></figcaption></figure></div>

<table data-view="cards"><thead><tr><th></th><th data-hidden data-card-cover data-type="image">Cover image</th></tr></thead><tbody><tr><td><mark style="color:red;"><strong>How to Build Odometry Wheels and Pods?</strong></mark></td><td><a href="https://www.vexforum.com/uploads/default/original/3X/0/a/0a91995d607fbf68fb225307e550a3d9105a77ea.jpeg">https://www.vexforum.com/uploads/default/original/3X/0/a/0a91995d607fbf68fb225307e550a3d9105a77ea.jpeg</a></td></tr></tbody></table>


{% endcolumn %}

{% column width="50%" %}
## Drivetrain Motor Encoders

This method uses the **built-in** [**motor encoders** ](#user-content-fn-1)[^1]on the drivetrain motors.

\
This method **doesn’t require additional sensors**, but it <mark style="background-color:$danger;">**may be less accurate than Odometry**</mark> because the inbuilt motor encoders (sensors) can be affected by wheel slip, traction changes, or external forces.

{% hint style="success" %}
<mark style="color:red;">**You will need no other sensors for this method as it uses your drivetrain motors sensor data.**</mark>
{% endhint %}

\
This method **doesn’t require additional sensors**, but it may be less accurate because the inbuilt motor encoders (sensors) can be affected by wheel slip, traction changes, or external forces.
{% endcolumn %}
{% endcolumns %}





<table data-card-size="large" data-view="cards"><thead><tr><th></th><th data-hidden data-card-cover data-type="image">Cover image</th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>Press Here if you are Using Motor Encoders for Autonomous Movements.</td><td><a href="https://kb.vex.com/hc/article_attachments/360042380051">https://kb.vex.com/hc/article_attachments/360042380051</a></td><td><a href="driver-controls.md">driver-controls.md</a></td></tr><tr><td>Press Here if you are Using Odometry Wheels for Autonomous Movements.</td><td><a href="../../.gitbook/assets/Screenshot 2025-12-03 at 12.24.41 am.png">Screenshot 2025-12-03 at 12.24.41 am.png</a></td><td><a href="configuring-odometry-in-c++.md">configuring-odometry-in-c++.md</a></td></tr></tbody></table>



[^1]: Basically Rotation Sensors
