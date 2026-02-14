# CAD Design

## 📏 CAD Design

> "Measure twice, cut once."

CAD (Computer‑aided design) is an essential part of VEX robotics. It lets teams fully plan out the robot on a computer before constructing anything in the real world.

CAD is a **tool**, not a requirement. If your team decides that the disadvantages outweigh the advantages, it’s okay not to CAD – but you should make that decision intentionally.

### Should we CAD?

#### Advantages of CAD

* Plans out the robot fully ahead of time
* Reduces the time it takes to build and iterate
* Makes it easier to communicate design ideas within the team
* Adds an element of professionalism to the engineering notebook (screenshots, exploded views, etc.)

#### Disadvantages of CAD

* Learning curve for new team members
* Can feel slower at first compared to just building
* Easy to over‑design in CAD without thinking about real‑world tolerances and build quality

### Choosing a CAD software

Onshape is the most commonly recommended software for VEX because of its ease of use, cloud collaboration, and existing VEX part libraries. However, Fusion 360 and Inventor also work well.

#### Common VEX CAD options

**Onshape**

| Pros                                                                                                                                                                     | Cons                                                                                     |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------- |
| <p>Easy to learn<br>Runs in a browser on almost any hardware (even Chromebooks)<br>Free for education<br>Cloud‑based and great for collaboration<br>User‑friendly UI</p> | <p>Fewer traditional CAD capabilities than some desktop tools<br>Limited offline use</p> |

**Fusion 360**

| Pros                                                                                                                                                                          | Cons                                                                                                                       |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| <p>User‑friendly UI<br>Can run on less powerful hardware than Inventor<br>Wide support options<br>Free / discounted educational access<br>Good built‑in tools for CAD/CAM</p> | <p>Must be installed on a computer (no pure browser version)<br>Stress‑simulation tools are more limited than Inventor</p> |

**Inventor**

| Pros                                                                                                                                                  | Cons                                                                                                                                                                   |
| ----------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>Very powerful, traditional CAD tool<br>Highly customizable workflows<br>Strong simulation tools<br>Free for students with an education license</p> | <p>Requires relatively powerful hardware<br>Primarily single‑user &#x26; local processing by default (you need external tools/cloud drives for easy collaboration)</p> |

### Introduction videos

Use these as a starting point if your team is new to CAD:

* Onshape for VEX overview
* Fusion 360 basics for VEX robotics
* Inventor introduction for robotics design

(Add or replace these bullets with your preferred videos.)

### VEX part libraries

* Onshape: VEX libraries are available directly inside most community VEX documents and public documents.
* Fusion 360: Download and import a VEX part library, then save it in your data panel for reuse.
* Inventor: Install or import a VEX parts library so you don’t have to model parts from scratch.

### How to use CAD (in practice)

CAD should capture **the important structure and mechanisms**, not every nut and screw.

* You usually **don’t need to model screws** or washers – it’s already clear where they belong.
* You **should model** the drivetrain, intakes, lifts, and any major mechanisms that affect geometry, spacing, and motion.
* Always remember that no robot has ever perfectly matched its CAD design. Real‑world tolerances, build quality, and on‑the‑fly changes will affect the final robot.

A good rule of thumb: **CAD anything that would be hard or expensive to change later.**

### Design tips

CAD design can be intimidating at first. A few guidelines help a lot:

* **Imitate, don’t copy.**\
  Watch matches, study reveal videos, and look at robots at tournaments. If you see a design you like, take inspiration from it and improve it—don’t copy it screw‑for‑screw.
* **Don’t overthink utility components.**\
  The exact locations of the brain, battery, and air tanks can often be figured out later and don’t always need to be modeled in early CAD versions.
* **Ask for feedback early.**\
  Get experienced members or mentors to review your CAD before you build. Catching problems in CAD can save hours of rebuilding.
* **Simpler is better.**\
  A well‑optimized simple design usually beats a complex one. Fewer mechanisms means fewer failure points.

#### VEX‑specific CAD tips

* Use **2–3 cross‑braces** on the drivetrain that span the full width/length of the robot, as far apart as possible. This keeps the chassis from bending over time.
* Use **standoffs everywhere** for bracing and mounting mechanisms. They are light, strong, and extremely versatile.
* Study how successful robots mount mechanisms to their chassis, then **adapt the idea** to your own design.

For drivetrain‑specific guidance, see [Drive Trains](drive-trains.md).

### Join the VEX CAD Discord server

The VEX CAD Discord server is a public community for VEX teams to ask questions, get feedback, and share designs.

* **Server invite:** https://discord.gg/BKV3DJm
