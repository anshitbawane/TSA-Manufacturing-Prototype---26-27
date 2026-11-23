# TSA Manufacturing Prototype: Display Case Project Context
 
Everything decided and researched in this chat, organized so it can be reused for parts research, the bill of materials (BOM), and the portfolio. Items marked **(est.)** are my estimates, not seller specs. Prices and stock change, so re-check before buying.
 
---
 
## 1. Project summary
 
- **Event:** TSA High School Manufacturing Prototype (2026-27 season).
- **Product:** A display case for a small collectible. A motorized lid lifts straight up at the push of a button to reveal the item.
- **Theme (from TSA's Themes and Problems page):** Display or container for small collectible items.
- **Look:** Industrial and rugged. Exposed metal on the scissor lift, a metal base, 3D-printed parts elsewhere, maybe some polycarbonate. All metal parts get finished.
- **Wow features:** A scissor-lift lid and a clear rotating base with LEDs that shows off the motor. A "hologram" screen on the lid is a side project.
## 2. Competition rules that affect design
 
| Rule | Detail |
|---|---|
| Size | Product and packaging must not exceed 15 x 15 x 15 in. **Decision: stay under 15 in in every state (open and closed).** Footprint should be about 13.5 in so the box walls and padding fit. |
| Processes | At least 2 CNC/CIM processes (CNC machining, laser engraving, 3D printing, vinyl cutting). Traditional methods are allowed in addition. |
| Major parts | 5 manufactured major parts, each with a drawing. |
| Packaging | Original design. **Only the team ID number may appear on it.** The prototype goes inside for submission. |
| Pitch (semifinal) | 2 minutes, 2-6 members. Must explain production cost per unit, materials, and price breaks. One double-sided 8.5 x 11 flyer allowed. **No electronic devices may be used in the pitch.** |
| Prelims | Judges score the prototype and packaging with no students present, so it has to work without you explaining it. |
| Rule violation | 20% deduction (or disqualification). |
 
**Scoring (260 points total):** Prototype 80 (Theme x3, Production Quality x3, Aesthetics x2), Packaging 20 (Appearance x2), Documentation Portfolio 110, Semifinal sales pitch 50.
 
**Portfolio pages, in order:** title page, table of contents, research photos, brainstorming sketches (1 page; more than 5 sketches earns the top band), isometric assembly drawing (11 x 17, folded), detail drawings, construction photos (max 2 pages), testing photos with captions (max 2 pages), bill of materials, Resources and AI Reflection (max 4 pages). Product testing and the isometric drawing count double.
 
## 3. Decisions made so far
 
- Scissor lift for the lid, driven by a motor and lead screw (the first idea, a CoreXY-style Z axis, was dropped).
- Load: 1 lb at the high end. Wants 5-8 in of lift and little clutter above the lid when closed.
- Rotating base, made clear, with LEDs inside to show the motor.
- Stepper motor for the lift and a small geared DC motor for the rotation (needs smooth speed, not position).
- CNC access: polycarbonate, wood, ABS, aluminum.
- Build the full case first. The hologram is developed on the side, with space left for it on the lid but never locked in.
- Packaging: a box (to be decided) with vinyl stickers (another CNC/CIM process).
- Price it as a high-quality metal prototype. 3D printing most of the bulk keeps cost per unit down.
- Advisor to be asked whether a built-in screen counts as an "electronic device" in the pitch.
## 4. How the design got here
 
**Original idea:** A CoreXY-style Z system (steppers, lead screws, rods) to lift the lid. My critique: over-engineered. 2 steppers, drivers, controller, T8 screws, rods, and bearings run about $60-100 (est.), racking is a risk on a lid, and it makes the cost-per-unit pitch look bad.
 
**Alternatives considered**
 
| Option | Pros | Cons |
|---|---|---|
| Linear actuator | Simplest true vertical lift, holds position, no firmware | Body is long, needs guide rods |
| Gear motor + string winch | Cheap, light | String stretches, can feel janky |
| Servo clamshell | Cheapest, most reliable | Not a straight lift, needs rear room |
| Spring/strut + solenoid latch | Dramatic, few electronics | Must be latched by hand, spring tuning |
| **Scissor lift** | Impressive, folds flat, holds without power | More parts, needs tuning, force is high near closed |
| Four-bar parallelogram | Strong, few parts | Arcs backward, needs rear space |
| 2:1 cable cascade with a short actuator | Short closed length | Cable stretch, needs guides |
| Rack and pinion | Strong, fast | Needs a lot of hidden height, gear alignment |
 
## 5. Linear actuator research (backup option)
 
Cheap actuators retract to roughly stroke + 4 in, so a 6 in stroke is about a 10 in body. That is why the scissor lift won.
 
- AMORACING 6 in, 1000N: https://www.ebay.com/itm/184365736331 (10 in retracted)
- Justech 6 in, 750N: https://www.newegg.com/p/3C6-05G2-02R97 (11 in retracted)
- VEVOR 6 in: https://www.vevor.nl/elektrische-ligstoelmotor-c_11593/vevor-6-inch-lineaire-actuator-hub-900n-dc-12v-voor-fauteuil-tv-lift-p_010178048847?lang=en
- Firgelli 6 in, 150 lb: https://eu.robotshop.com/products/firgelli-12vdc-6-inch-stroke-150lb-premium-force-linear-actuator
- Mini 12V 150 mm (about stroke + 55 mm closed, per one listing): https://funduinoshop.com/en/electronic-modules/electric-motors-and-accessories/servo-motors/linear-actuator/like-hydraulic-cylinder-12v-150mm-20n/40n/60n/120n
- Pololu Glideforce GF01 100 mm, $74.95: https://www.pololu.com/product/4471/specs
- Actuonix L12 100 mm: https://ca.robotshop.com/products/actuonix-l12-12v-100mm-1001-plc-rc-miniature-linear-actuator
## 6. Scissor lift design notes
 
**Geometry** (N stages, arm length L, angle θ from horizontal):
- Lift = N x L x (sin θmax - sin θmin)
- Screw travel = L x (cos θmin - cos θmax)
- Example: 2 stages, 6 in (152 mm) arms, 10° to 40° gives about 143 mm (5.6 in) of lift with only about 33 mm (1.3 in) of screw travel.
**Force on the screw:** about N x weight / tan θ. For 2 lb (8.9 N) total and 2 stages:
- 10°: about 100 N (22 lbf)
- 15°: about 67 N (15 lbf)
- 40°: about 21 N (5 lbf)
Keep the minimum angle at about 12-15° to cut the force. The lid moves fast near closed and slowly near open, so ease the motor in.
 
**Build advice**
- Double scissor (one on each side) tied with a cross rod to stop twisting.
- Arms in 1/8 in aluminum or ABS. Avoid polycarbonate for arms (cracks near holes). Use polycarbonate for panels.
- Pivots: shoulder screws or steel dowels with bushings. Do not run threaded bolts through bare holes.
- The sliding top ends ride in slots under the lid.
- Don't let the arms fold fully flat.
**Examples to learn from**
- Sam Baker's 3D-printed projector lift (stepper plus lead screw): https://hackaday.io/project/190313-projector-lift-for-home-theaters
- Instructables scissor lift: https://instructables.com/Raspberry-Pi-Controlled-Scissor-Lift
- MakerWorld double scissor: https://makerworld.com/en/models/3364346
- Two unverified YouTube links: https://www.youtube.com/watch?v=QUb85goys3Y (small motorized scissor lift) and https://www.youtube.com/watch?v=G30edgY6RIA (3D-printed linear actuator, not a scissor).
## 7. Lead screw drive (parts and why)
 
**Recommended screw: T8 x 2 mm lead** (8 mm / 0.315 in diameter, 1-start, 2 mm pitch and lead), stainless, 150 mm (5.9 in) long. Lead = pitch x number of starts. A listing like "T8x8 (P2)" means 4 starts.
 
| Screw | Lead | Turns for 33 mm | Time at 3 rev/s | Steps/mm (1/16) | Thrust (est.) | Holds when off? |
|---|---|---|---|---|---|---|
| T8x2 | 2 mm (0.079 in) | 16.5 | about 5.5 s | 1600 | 125-200 N | Yes |
| T8x4 | 4 mm (0.157 in) | 8.3 | about 2.8 s | 800 | 90-140 N | Marginal |
| T8x8 | 8 mm (0.315 in) | 4.1 | about 1.4 s | 400 | 55-85 N | No, may creep |
 
**Parts, motor to far end**
 
| Part | Spec | Role |
|---|---|---|
| Stepper motor | NEMA 17, 5 mm D shaft, 4 M3 holes on a 31 mm square | Turns the screw |
| Flexible coupler | 5 mm to 8 mm bore, about 25 mm long | Joins shaft to screw, absorbs misalignment |
| Lead screw | T8 x 2, 150 mm | Converts rotation to linear motion |
| Thrust bearing and bracket | About 8 x 16 x 5 mm, flat | Takes the axial load so the motor's bearings don't |
| Shaft collar | 8 mm bore, set screw | Locks the screw against the thrust bearing |
| Brass nut | T8 x 2 flange nut, about 22 mm flange | Rides the screw, pulls the scissor pivot |
| Nut carriage | Printed or CNC aluminum | Holds the nut, links to the sliding pivot |
| End bearing | 688ZZ, 8 x 16 x 5 mm | Supports the far end (let it float) |
| Limit switch | Micro switch with lever | Homing and end stop |
 
**Key points:** Put the thrust bearing and collar at the motor end. Stepper shaft bearings usually allow only about 10-25 N axial force (check the datasheet). Hold the nut so it can't spin, guide the carriage so it only slides, and grease the screw with PTFE or white lithium.
 
An interactive 3D explorer of these parts: https://claude.ai/artifact/Gpa6Tg9Kq9mogATJsNZegU
 
## 8. Motors
 
| Spec | NEMA 17 (17HS4401), lift | N20 12V 298:1, rotation | Olimex MG-12V-12RPM, backup |
|---|---|---|---|
| Type | Bipolar stepper, 200 steps/rev | Brushed DC, metal gearbox | Brushed DC gearmotor, 500:1 |
| Voltage | 12-24V via driver | 12V | 12V |
| Current | 1.5-1.7 A per phase (run about 1 A) | under 40 mA no-load, under 0.1 A rated | 50 mA free, 1.2 A stall |
| Torque | 40 N·cm holding | 1.2 kg·cm rated, 2.6 stall | over 24 kg·cm stall |
| Speed | about 60-300 rpm best (est.) | 50 rpm no-load, 28 rated | 12 rpm |
| Size | 42 x 42 x 40 mm | 12 x 10 x about 26 mm | 25 mm round x 57 mm |
| Weight | about 280-300 g | about 10-18 g | not listed |
| Price | about $10-15 (est.) | about $7-9 (est.) | about 5 EUR |
| Needs | Stepper driver (TMC2209, A4988) | DC driver (DRV8833 or MOSFET) | Same |
 
- N20 pick: https://ca.robotshop.com/products/n20-micro-metal-gearmotor-w-20mm-length-m3-screw-shaft-12v-50rpm
- Olimex backup: https://olimex.com/Products/Robot-CNC-Parts/Micro-Motors/MG-12V-12RPM
- A turntable looks best at about 3-8 rpm. Run the N20 at lower voltage with PWM and add a 3:1 or 4:1 printed or CNC gear stage, which also looks good through the clear base.
- Put the turntable weight on a bearing (lazy-susan or thrust type). Don't stall small gearboxes on purpose.
## 9. Electronics and wiring
 
- **Base (always on):** Lift motor, rotation motor, limit switch, button, LEDs, power supply, and a small controller (Arduino Nano or ESP32).
- **Lid (screen side):** Screen plus its own controller, powered by a thin cable from the base.
- **Why split:** Power through a scissor lift is easy (2 wires), but screen data is not.
- **Trigger options:** One extra signal wire (lid up = HIGH), or two ESP32s over ESP-NOW (wireless, one more thing that can fail).
- **Cable routing:** Coiled cable, or flexible silicone stranded wire along one arm with a slack loop at each pivot. Not solid wire.
- **Power:** Give the lid its own 5V regulator, separate from the motor rail, to avoid screen flicker. Use 22-24 AWG stranded wire for about 1-1.5 A.
- **LEDs:** Keep them on the stationary part of the base so no slip ring is needed.
- **Skip:** A battery in the lid. Wired power is safer when judges operate it alone.
## 10. Hologram pyramid (side project)
 
- An acrylic four-sided pyramid under a downward-facing screen shows details about the item.
- Needs a dim environment and a black-background video. A bright LED inside will wash it out.
- Adds weight to the lid. Plan for about 1 lb or find a stronger lift.
- The "no electronic devices" pitch rule may be a problem. Ask the advisor first.
- Alternative: an engraved or printed plaque (another CNC process).
## 11. Packaging, pricing, pitch
 
- A box with vinyl stickers. Stickers may only show the team ID number or pure decoration. Packaging vinyl does not count toward the prototype's 2-process requirement.
- Build the BOM as you go. The metal arms and base will probably be the biggest cost. Be ready to explain how price drops at larger quantities.
## 12. Portfolio files made in this chat
 
- Sample 8.5 x 11 brainstorming page (PDF and SVG), six boxed sketches. Replace with your own work.
- Image-generator prompt for a hand-doodled version, with no boxes, scattered doodles.
- The interactive lead screw explorer (link in section 7).
## 13. Open questions and next steps
 
- What item is being displayed (its height sets the lift)?
- What does the lid weigh (screen, panels, frame)?
- Arm length and stage count for the scissor.
- Screen type and size for the hologram.
- Advisor answers on the screen/electronics rule.
- Your state's portfolio deadline.
- Start documenting now: construction photos, test photos with captions, more than 5 sketches, and the BOM.
- Specific part listings for the stepper driver, thrust bearing, coupler, and turntable bearing are not yet chosen.
