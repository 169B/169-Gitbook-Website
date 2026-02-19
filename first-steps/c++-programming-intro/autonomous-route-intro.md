---
description: Plan your autonomous first, then code it.
---

# Autonomous Route Intro

Autonomous code is **planned**, then **written**, then **tested**.

If you skip the plan, you’ll waste practice time guessing distances.

***

### The overall process

{% stepper %}
{% step %}
### Step 1 — Decide the goal

Pick **one main objective** for match autonomous.

Examples:

* “Secure an early score, then park.”
* “Grab one game object reliably, score it, then go to another specific one.”

{% hint style="info" %}
Reliable points beat “almost worked once” every time.
{% endhint %}
{% endstep %}

{% step %}
### Step 2 — Copy good ideas (fast)

Watch a few good match runs on YouTube for that season.

Look for:

* Where they **start**
* What they score **first**
* What they ignore (often the best clue)

Write down 2–3 patterns you like.

#### **Some helpful YT Channels:**

Robo Stats is great for seeing very developed, complex and winning autos[^1] by good teams. They record both driver and autos of signature event elimination matches:

{% embed url="https://www.youtube.com/@robotstats" %}

Just Search "push back auto" on YT for posted routes:

{% embed url="https://www.youtube.com/results?search_query=push+back+auto" %}
{% endstep %}

{% step %}
### Step 3 — Sketch the route

Draw the field and your robot start position.

Then draw a route:

* Drive segments
* Turns
* “Do mechanism thing here” such as intake a game object.

Add rough labels like `+24"`, `-12"`, `90°`.

{% hint style="info" %}
## Field Tiles are exactly 24 inches long and wide!
{% endhint %}

{% hint style="warning" %}
If you can’t explain the route out loud, don’t code it yet.
{% endhint %}

### Helpful Extras - Unneeded:

Use a route planner like [jerry.io](https://jerry.io). (Steep Learning Curve)

Use it to turn your sketch into:

* Distances (inches)
* Headings (degrees)
* A clean list of “checkpoints”


{% endstep %}

{% step %}
### Step 4 — Turn checkpoints into code

In most templates, autonomous lives in `autons.cpp`.

You’ll write the route as a sequence of:

* Drive to a distance
* Turn to an angle
* Run intake / pistons / lift at the right times

Keep each autonomous routine **short** and **named**.
{% endstep %}

{% step %}
### Step 5 — Test, then simplify

Run the autonomous 10 times.

Track:

* Miss distance (short/long)
* Turn error (left/right)
* What step fails first

Then simplify:

* Remove risky steps
* Increase spacing
* Add small waits only where needed
{% endstep %}
{% endstepper %}

***

### What “good autonomous” looks like

* Scores **some points** even when imperfect.
* Doesn’t rely on “perfect field setup”.
* Still works after battery changes and small bumps on the field.

Next, you’ll start coding your first route in `autons.cpp`.

[^1]: Short for Autonomous
