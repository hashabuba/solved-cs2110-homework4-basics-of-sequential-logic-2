Download Link: https://assignmentchef.com/product/solved-cs2110-homework4-basics-of-sequential-logic-2
<br>
In this assignment, you will learn the basics of sequential logic, and create both a one-hot state machine and a reduced state machine.

<a name="_Toc6331"></a>Part 1: RS Latch, Master-Slave D Flip-Flop, and Register

For this part of the homework you are going to make your own Register, from the ground up. All of the circuits in this part will be in the latches.sim file.

RS Latch

Open up the the RS Latch subcircuit in the latches.sim file. For this part you will need to create an RS Latch. <strong>Note</strong>: You only need 1 output, so you may disregard the inverse output of a normal RS Latch.

<strong>You can find information about this circuit in the Patt &amp; Patel textbook, pages 65 and 66.</strong>

Master-Slave D Flip-Flop

Open up the D Flip-Flop subcircuit. For this part you will need to create a Master-Slave D Flip-Flop using the RS Latch you just created. <strong>Note</strong>: Your implementation of this Master-Slave D Flip-Flop should use only change on the <strong>rising edge</strong>, i.e, the state of the D Flip-Flop should only be able to change at the exact moment when the CLK (Clock) input goes from 0 to 1.

<strong>Consider implementing a Gated D Latch subcircuit first.</strong>

Figure 1: An example of the Master Slave D Flip Flop, with the boxes representing Gated D Latches

<strong>You can find information about the Gated D Latch and this circuit in the Patt &amp; Patel textbook, pages 65 and 66.</strong>      Register

Open up the Register subcircuit. For this part you will need to create a <strong>4-bit </strong>Register. This Register also needs to use edge-triggered logic. <strong>Hint</strong>: Split the 4-bit input and utilize the D Flip-Flops you just created.

<a name="_Toc6335"></a> Part 2: Finite State Machine

For this part of the homework, you will implement the finite state machine behind a parking garage gate.

The State Machine

We are modeling the finite state machine behind a boom barrier (think gated parking garage entrances).

<h3><a name="_Toc6337"></a>2.1.1         Scenario</h3>

<ol>

 <li>State: We start with the barrier closed, there is no car, and the SCAN YOUR BUZZCARD light is on.</li>

 <li>Event: A car approaches the machine and the driver scans their card.</li>

 <li>State: The barrier opens and stays open.</li>

 <li>Event: The driver drives under the gate, the sensor under the gate starts showing that there is a car underneath.</li>

 <li>State: The barrier stays open, waiting for the car to pass.</li>

 <li>Event: The driver clears the gate, and the sensor under the gate starts showing that there is not a car underneath.</li>

 <li>Our state machine loops back to the beginning, with the gate closed and light on.</li>

</ol>

Figure 2: Our state machine with its 3 states in order.

<h3><a name="_Toc6338"></a>2.1.2         States</h3>

Our state machine has 3 states: <strong>State 0: Gate Closed</strong>, <strong>State 1: Gate Open</strong>, and <strong>State 2: Car Under Gate</strong>. Our state machine begins with <em>State 0: Gate Closed</em>.

<h3><a name="_Toc6339"></a>2.1.3         Inputs</h3>

<ul>

 <li><em>G </em>= Valid card scan from card scanner (1 when a valid card scan has been made, 0 otherwise)</li>

 <li><em>F </em>= Gate sensor: whether or not there is a car passing under the gate (1 when a car is underneath the gate, 0 otherwise)</li>

</ul>

<h3><a name="_Toc6340"></a>2.1.4         Outputs</h3>

<ul>

 <li><em>A </em>= <em>Scan Card Now </em>light at the kiosk</li>

 <li><em>B </em>= Signal to the motor to keep the gate open</li>

 <li><em>C </em>= Signal to the motor to keep the gate closed</li>

</ul>

<strong>Note that B and C are the inverse of each other and there’s no practical reason why you’d do this in real life. They exist just for the sake of having more outputs.</strong>

<h3><a name="_Toc6341"></a>2.1.5         State – Output Mappings</h3>

<ul>

 <li>State 0: Scan card light and closed garage door</li>

 <li>State 1: Open garage door</li>

 <li>State 2: Open garage door</li>

</ul>

<h3><a name="_Toc6342"></a>2.1.6         Transitions</h3>

<ol>

 <li>If we are in state 0 and <em>G </em>== 1 (a card was read) we transition to state 1.</li>

 <li>If we are in state 1 and <em>F </em>== 1 (a car is detected underneath) we transition to state 2.</li>

 <li>If we are in state 2 and <em>F </em>== 0 (the detected car is gone) we transition to state 0.</li>

</ol>

<strong>Note that these rules don’t include every possible combination of inputs and current state. </strong>You should interpret these rules as sufficient – for example, if we are in state 0 and <em>G </em>== 1, we should transition to state 1 regardless of the value of <em>F</em>. Similarly, all input combinations not containing <em>G </em>== 1 at this state should result in staying in this state.

<h3><a name="_Toc6343"></a>2.1.7         Finite State Machine Diagram</h3>

Here is a diagram of our state machine containing all of the information listed above:

Figure 3: The State Machine Diagram for our State Machine

<h2><a name="_Toc6344"></a>2.2         One-Hot Encoding Implementation</h2>

For this part of the homework you will need to implement our state machine in CircuitSim using a <strong>One-Hot Encoding</strong>. What this means is that we use 1 bit per state to represent our current state. So with our 3 states, we will need 3 bits. <strong>It is important that this machine stays one-hot: there should be at most one bit set to 1 in the register at any time</strong>.

Use the following mappings for each state in your One-Hot state machine:

<ul>

 <li>State 0: 001</li>

 <li>State 1: 010</li>

 <li>State 2: 100</li>

</ul>

Make this circuit in the One-Hot State Machine subcircuit in the fsm.sim file. Also, notice along with <em>G </em>and <em>F </em>there are 2 other inputs: CLK is the clock and will be used to simulate the clock of the circuit cycling on and off, and RESET should reset your state machine.

<strong>Your state machine, when the circuit is initially started or when the reset button is pushed, will return to the invalid 000 state. You need to handle this case to make it go to State 0, which is our start state.</strong>

<h2><a name="_Toc6345"></a>2.3         Reduced Encoding Implementation</h2>

For this part of the homework you will need to implement our state machine in CircuitSim using a <strong>Reduced Encoding</strong>. This means we will be using two bits to represent the state instead of the three bits we used in the One-hot case.

<strong>Each state will be represented by its number in two-bit binary: State 0 corresponds to </strong>00<strong>, State 1 to </strong>01<strong>, and State 2 to </strong>10<strong>. The </strong>11 <strong>encoding is unused.</strong>

<h3><a name="_Toc6346"></a>2.3.1         Worksheet</h3>

In order to reach this encoding, you need to prepare a truth table, Karnaugh maps, and finally reach the final reduced expressions that you will use for the gates in your circuit. For this purpose, we have prepared a worksheet that you will find in this archive that you must complete. This worksheet will be scanned and submitted on Gradescope, and its contents will be written on Canvas for autograding. Please follow instructions on the worksheet for more information. <strong>You MUST complete the worksheet.</strong>

<strong>IMPORTANT! SUBMIT YOUR WORKSHEET CONTENTS ON CANVAS TO SEE THAT YOU HAVE GOTTEN IT RIGHT BEFORE CONTINUING.</strong>

<h3><a name="_Toc6347"></a>2.3.2         Circuit</h3>

Now that the worksheet is complete and you have verified your results on Canvas, it’s time to implement this circuit in the Reduced State Machine subcircuit in the fsm.sim file. Also, notice along with <em>G </em>and <em>F </em>there are 2 other inputs: CLK is the clock and will be used to simulate the clock of the circuit cycling on and off, and RESET should reset your state machine.

<strong>Since </strong>00 <strong>is the default state, no additional logic for the resetting is required in this case.</strong>

<h1><a name="_Toc6348"></a>3           Deliverables</h1>

Please make sure the following items have been submitted in the correct locations:

<ol>

 <li><strong>Worksheet contents </strong>⇒ Canvas, submission details on Worksheet</li>

 <li><strong>Worksheet scan </strong>⇒ Gradescope, <em>Homework 4 Worksheet Scan </em>assignment</li>

 <li>sim and latches.sim⇒ Gradescope, <em>Homework 4 Circuits </em>assignment</li>

</ol>