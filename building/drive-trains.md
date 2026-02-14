# Drive Trains

## Drive Trains

Drive trains are not technically required, but nearly every robot has one. The drivetrain lets the robot traverse the field and serves as the **foundation** for the rest of the robot.

### Common drivetrain types

#### Simple tank drive

This is the most common and usually the most competitive option.

* At least 2 omni wheels on each side of the robot (often 4 or 6 total).
* Typically powered by 4–6 motors, either directly or through gears.
* Can turn in place and move forward/backward, but **cannot strafe** sideways.

A well‑built tank drive is strong, reliable, and easy to program.

#### X‑drive

An X‑drive uses wheels mounted at 45° so the robot can **strafe** (move sideways) as well as forward/backward.

Pros:

* Excellent maneuverability.
* Can dodge defense and make precise lateral adjustments.

Cons:

* Reduced torque and pushing power compared to a tank drive.
* More complex mechanically and in code.
* Weaker in heavy defense situations.

For example, during Spin Up Worlds, all of the division‑winning robots used tank drives rather than X‑drives, largely because of the importance of pushing power and robustness.

#### Other drivetrains

There are many other concepts (H‑drives, mecanum, holonomic variants, etc.), but most are **not competitively viable** in the constraints of VEX Robotics (weight, part limits, friction, code complexity, etc.).

Overall, for both new and experienced teams, the **recommended drivetrain is a standard tank drive**.

### Design guidelines for tank drives

Assuming you’re going with a tank drive (you should strongly consider it!), keep these guidelines in mind when designing:

* **Smaller is generally better.**\
  A compact chassis accelerates quickly and turns easily – but don’t make it so small that you can’t fit mechanisms on top.
* **Minimize gears.**\
  Use as few gears as possible to reduce friction and slop. Direct drive or a single reduction is often ideal.
* **Spread the wheels out.**\
  Keep front and back wheels as far apart as reasonable – this increases stability and reduces tipping.
* **Brace the chassis well.**\
  Use 2–3 cross‑braces across the full width/length of the robot, as far apart as possible. This keeps the frame square and resists bending under defense.
* **Square the chassis carefully.**\
  A square, low‑friction chassis is critical for consistent autonomous and smooth driving.

Always **CAD the drivetrain before building it** so you can:

* Check motor placement and gear clearance.
* Verify wheelbase dimensions and ground clearance.
* Plan mounting points for mechanisms.

For CAD guidance, see [CAD Design](cad-design.md).

### Additional resources

* Tutorials on squaring and bracing VEX drivetrains.
* Example tank drive CADs from top teams.
* Drivetrain friction‑reduction guides (bearing alignment, shaft choice, lubrication, etc.).

(Add links or videos here that your team finds most useful.)
