🏁 Final Project: Button Race – STM32F401RE
🎯 General Objective
Develop a simple competitive embedded video game using the STM32F401RE microcontroller, where one or two players compete by pressing a button as fast as possible to advance an animated character in a race displayed on a 16x2 LCD. The project integrates concepts such as GPIOs, external interrupts (EXTI), timers, PWM, and advanced LCD handling (CGRAM, display shift).

⚙️ Technical Specifications
🔹 Base Version – up to 75 points
Goal: A single-player race where the player competes against themselves to complete a predefined route on the display.

Requirements:

Race start:

The character starts at coordinate (0,0) on the LCD.

As it moves forward, it should leave a visible trail of its path on the screen.

Race path:

When reaching (0,15), the character must "turn" and move down to (1,15) and continue to the left until reaching (1,0).

The complete path forms an inverted "U" shape.

Dynamic speed and movement:

The character’s movement depends on button press frequency (presses per second):

> 8 presses/sec → Advances 1 position every second.

Between 4 and 8 presses/sec → Takes 2 seconds to move one position.

< 4 presses/sec → The character moves backward one position per second.

(This logic is feasible using a sliding time window of 1 second and counting presses within that window.)

PWM duty-cycle control:

A PWM signal must represent the percentage of progress in the race.

Example: 50% race completion → 50% duty cycle.

Victory animation:

When the character reaches (1,0):

The LCD displays a blinking or animated victory message.

PWM enters a “celebration” pattern (blinking, fading, etc.).

🔹 Extended Version – up to 100 points
Goal: Two-player competitive mode, with enhanced visuals and gameplay mechanics.

Additional Requirements:

Two-player mode (one per LCD line):

Player 1 on line 0, Player 2 on line 1.

Each player has an independent button with its own EXTI.

Display shift:

Players advance through 40 positions, not just the 16 visible.

The LCD display content must shift to simulate movement through a longer track.

Trailing player indicator:

If a player falls behind and their character goes out of the visible area,
a blinking arrow must appear on the edge of the screen to indicate they’re off-screen.

Independent PWM for each player:

Each player controls a separate PWM signal (two timers/channels).

PWM intensity reflects each player’s progress.

Time-limited race (against the clock):

The race must be completed within a fixed time limit (e.g., 30 seconds).

If no one finishes, either show a draw or declare the furthest player the winner.

📝 Evaluation Criteria
Criterion	Description	Max Score
Basic LCD progress with trail	Character moves correctly with visible path	15 pts
Correct U-shaped path (0,15 → 1,15 → 1,0)	Full route is properly followed	10 pts
Dynamic speed logic (advance/retreat)	Correct interpretation of press frequency to move the character	15 pts
PWM representing race progress	PWM duty cycle correctly maps to progress	10 pts
Victory animation on LCD and PWM	Victory message and PWM pattern when finishing	10 pts
Code modularity and clarity	Well-structured and commented code	15 pts
Extended version implemented	All additional features working properly	+25 pts

🧠 Note: Students can score up to 75 points with a solid base version. Full 100 points require implementing all extended features.

📦 Submission Requirements
Source code files (.c, .h, or .ino)

Schematic diagram (Proteus or physical wiring)

Short demo video (recorded physically or from Proteus simulation)

PDF report (1–2 pages) briefly explaining logic, structure, and technical solutions
