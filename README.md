# GOAL-E
#### MTE 481 — Mechatronics Engineering Design Project
_Andrew Willms, Christian Bergmann, Erik Smith, Jonathan Gervais, Josh Cooke_

test change

&nbsp;
## Problem Formulation

### The Needs We Have Observed
- Hockey goalies are often in very high demand for training.
- Many types of practice (such as shooting practice):
  - are very tiring for the goalie,
  - pose a substantial injury risk to the goalie, and
  - are not valuable training for the goalie.
- This leads to goalies not wanting to practice for long or deliberately missing practice.
- Current tools to substitute for goalies are simple static elements. These elements:
  - are a poor substitution, providing less valuable practice and
  - are less engaging, leading players not making a full effort.
- Baseball has created realistic pitching systems that enable hitters to practice without a pitcher. 
- Creating a similar tool for hockey would:
  - reduce goalie fatigue
  - reduce goalie injury risk
  - enable types of practice that pose a high risk of injury to goalies (such as slapshot practice)
  - increase player engagement during drills
  - greatly increase the amount of time players are able to practice

&nbsp;
### Problem Statement
Create a reactive hockey training device for players to practice against, removing the need for a human goalie.

### Functions and Goals
- Must be able to block, deflect, or capture pucks that are shot towards a hockey net.
- Must be able to operate autonomously.
- Must have an e-stop button accessible from behind the net and from a remote.
- Must sense the position of the puck before it is shot and move to minimize the open portion of the net.

### Constraints
- IP54 water and dust resistance.
- Must be able to operate in temperatures from -20°C to 40°C.
- Must be able to withstand repeated 80km/h slapshots.
- Must be electrical safety approved.
- Must be able to be powered off of a single 10A, 120V circuit.
- Must be able to complete the project before symposium.

### Objectives
- Complete the project using a total budget of $3000 or less.
- Be able to move across the crease in 2 seconds or less.
- Be able to identify unobstructed pucks within 20m with an accuracy of 95% or greater.
- Be able to identify pucks and estimate their postion in 50ms.
- Be able to identify the position of the puck within 5% of the distance to the puck.
- React correctly to 95% of unobstructed 50km/h shots taken from 3-20m away.
- Obstruct the same area of the net as an average junior or adult goalie.
- Be vulnerable to and effective against the same scoring strategies that human goalies are.
- The design should encourage players to play against it in the same way they would play against a human goalie.

### Criteria
- Cost (CAD)
- Effort to complete (/10)
- Cross-crease time (s)
- Puck identification accuracy (%)
- Puck position estimation time (s)
- Puck position estimation accuracy (%)
- Human-like feel and effectiveness (/10)

&nbsp;
## Design

(figuring pending)<br>
Our design is a human silouette with moving goalie pads on the end of 2-degree of freedom robotic arm. The arm will be able pivot about a central point and telescope to become longer or shorter. These two motions should be sufficient to place the sillouette in the positions and orientations that a human goalie would most often occupy.
We roughly estimate that the human silouette will have a mass of at most 30kg and the telescoping arm will extend from 0.8m to 1.5m.

### Acceleration Requirements
Our objectives dictate that the system needs to be able to move from one side of the crease to the other in two seconds. If we assume that acceleration and decceleration are approximately symetrical, this means the human sillouette needs to be able to move from one side of the crease to the center of the crease in at most one second. Based on our initial drawings, this motion is about 60 degrees or one radian. Using these values (30kg load on the end of a 1.5m arm) we were able to simulate the approximate perforance different combinations of motors and speed reducers would yield. The figure belows shows the performance of three Rev Neo 1.1 with a 100:1 reduction (motor selection explained beow). The green line crosses the one radian mark at approximately 400ms meaning this design theoretically meets the objective with a safety factor of 2.5.<br>
<img width="1000" height="640" alt="Motor Dynamics Graph" src="https://github.com/user-attachments/assets/ff731feb-146f-4995-8941-8ecf562d2c62" /><br>

### Motor Selection
We selected the [Neo Brushless 1.1](https://www.revrobotics.com/rev-21-1650/) as our primary motor because our group has access to a large number of them at a heavily discounted price. The key specifications of these motors are:
- Nominal Voltage: 12 V
- Empirical Free Speed: 5676 RPM
- Empirical Stall Torque: 2.6 Nm
- Empirical Stall Current: 105 A
We plan to use three or four Neos to power the pivot point, two to power the telescoping of the arm, and two more to move the goalie pads.

### Worst-Case Power Consumption Senario
From our performance specifications we estimate a worst-case power draw to be:
- 4 motors actuating the pivot point drawing stall current (105A, from motor specs)
- 2 motors actuating the telescoping arm drawing stall current (105A, from motor specs)
- 2 motors actuating the goalie pads drawing high current (40A, estimated)

The math to calculate the system's peak current and power draw is shown below:<br>
<img width="509" height="106" alt="image" src="https://github.com/user-attachments/assets/7e72ae40-5636-4826-98a1-9f44c1cbd240" /><br>
Since 8520W is well in excess of the 1800W a 10A, 120V circuit can provide, the system must have onboard power source to supply power during peak load. We explored the possibility of using a battery bank as a buffer that would augument a (wall circuit driven) switching power supply while load was high and could be rechared while load was low. Unfortunately, due to electrical safety requirements and the added complexity of adding a charging circuit, we determined it would be far more achieveable to have the system run directly off battery power.

### Battery Selection
We selected the [MK Battery ES17-12](https://www.revrobotics.com/rev-19-2487/) as the batteries to use in the battery bank because our group has access to a large number of them at a heaviliy discounted price. The key specifications of these batteries are:
- 12 V nominal (13 - 13.6V actual)
- 270 A discharge for up to 5 seconds
- 120 A continuous discharge
- Internal resistance of 12 milliohm
- 18 Ah

### Control System Dynamis
The dynamics of the central pivot point are expression in the figure below. The equats on the right relate the input power of the motor, u, to the position, θ, of the the system at the next time increment. <br>
<img width="1000" height="772" alt="image" src="https://github.com/user-attachments/assets/3fb49c00-3cf8-47bb-91f9-60546dca63fd" /><br>

### Robot CAD
<img width="749" height="539" alt="Robot CAD" src="https://github.com/user-attachments/assets/73900b14-25f3-4af4-a5a4-7ddfd4cfca02" />
<img width="270" height="349" alt="Robot CAD 2" src="https://github.com/user-attachments/assets/d0b1bd21-50a3-418b-9459-3ad0e46f9a89" />
<img width="310" height="178" alt="Robot CAD 3" src="https://github.com/user-attachments/assets/e3bb54dc-2d5e-415d-abad-bfb548565963" />
<img width="372" height="167" alt="Robot CAD 4" src="https://github.com/user-attachments/assets/5cba4348-3139-45ed-b63e-815cf4ec3640" />

&nbsp;
## Design Log

| **Week** | All | Andrew Willms | Christian Bergmann | Erik Smith | Jonathan Gervais | Josh Cooke |
| -------- | --- | ------------- | ------------------ | ---------- | ---------------- | ---------- |
| 09/07    | Created the problem statement. | Consulted professor [Russell Buchanan](https://uwaterloo.ca/mechanical-mechatronics-engineering/profile/r6buchan) about CV options.<br> Sourced IR lights and cameras for evaluating CV implementations. | Set up project management processes. | Started compiling a list of solution agnostic materials (e.g. power supply, generic construction materials) to obtain a rough budget estimate. | Spoke with hockey players and coaches to asses community needs. | CADed hockey net and crease to improve our understanding of the physical constraints of a hockey rink. |
| 09/14    | Finalized constraints and criteria. | Began construction of a test rig for the vision system. | Constructed a small scale visual model of the net to aid in visualization of size and angles. | Researched motor and motor control options. | Created motor torque calculator to help evaluate the theoretical performance of different motors and gear reduction combinations. | Lead creating the constraints and criteria. |
| 09/21    | Brainstormed designs.  | Compared the amount of ambient light in 850 and 940nm wavelengths. | Reached out to more hockey teams and players and collected quotes. | Worked on sketches for the design proposal. | Worked on sketches for the design proposal. | Worked on preliminary designs. |
| 09/28    | | Began creating CV application to gather and process test footage. | Contacted the Motion Research Laboratory and [John McPhee](https://uwaterloo.ca/systems-design-engineering/profile/mcphee) regarding the possibility of borrowing motors. | Worked on sketches for the design proposal. | Worked on sketches for the design proposal. | Contacted the Motion Research Laboratory and [John McPhee](https://uwaterloo.ca/systems-design-engineering/profile/mcphee) regarding the possibility of borrowing motors. |
| 10/05    | Preparation for preliminary design presentation | Developed slides for constraints, objectives and criteria. | Compiled gathered quotes for presentation. Updated gantt chart for presentation. Created slides for patent analysis. | Updated sketches for presentation and created related slides. | Updated sketches for presentation and created related slides. | Created slides for problem statement and opening of presentation. |
| 10/12    | Reading week. PDP preparation. | | | | | |
| 10/19    | Midterms | | | | | |
| 10/26    | Design analysis and calculations. | Researched control system options and derived formulas for system dynamics. Sourced motors and speed controllers for testing. Aided in torque and electrical power requirement calculations. | Aided in motor torque analysis. Developed CAD for the goalie and the arm mechanism. | Researched power supply options, calculated voltage and current requirements, and worked on electrical schematics. | Aided on more in depth conceptualization of goalie mechanism on end of arm, relating to motion of arms and lower body. | Finalized torque requirements and ideal gear ratios. Began designing a capstan speed reducer to meet the torque requirements. |
| 11/02    | Team focus on electrical design and finding a solution to the high current requirements. | | Consult with varsity players on what features would be most useful. | | | |
| 11/09    | | Selecting and sourcing RGB cameras to replease the IR camera system that was initially selected. | Selected and sourced a Jetson Nano as a vision co-processor. | Designing low voltage system to power the Arduino and Jetson Nano. |  Detailed CAD work. | Detailed CAD work. |
| 11/16    | Final Design Presentation | | | | | |
| 11/23    | Final Design Report | | | | | |
| 11/30    | Final Design Report | | | | | |
