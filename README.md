# 🏁 Button Race Game – Final Project (STM32F401RE)

A simple two-player embedded video game for the STM32F401RE microcontroller. Players compete by pressing their buttons as fast as possible to move their animated runner across the LCD screen. The game features character animation, race progress tracking via PWM, external interrupts, and advanced LCD manipulation including display shifting.

---

## 🎮 Project Description

Each player controls a character displayed on their respective line of a 16x2 LCD display. The characters move from left to right as players press their buttons. The faster you press, the faster your character moves. The game uses external interrupts (EXTI) to detect button presses, and timers to calculate press frequency and generate PWM signals proportional to race progress.

---

## 🧩 Features

### ✅ Base Version
- Single-player race from `(0,0)` → `(0,15)` → `(1,15)` → `(1,0)`
- Character leaves a visible trail behind.
- Movement speed depends on press frequency:
  - **> 8 presses/sec**: Move 1 cell every second.
  - **4–8 presses/sec**: Move 1 cell every 2 seconds.
  - **< 4 presses/sec**: Character moves **backward** 1 cell per second.
- PWM output intensity reflects race progress (e.g., 50% complete → 50% duty cycle).
- Victory animation on LCD and PWM output when the player finishes the race.

### ⭐ Extended Version
- Two-player competitive mode (Player 1 on line 0, Player 2 on line 1).
- Display shifting used for extended 40-character track.
- Blinking arrow shows if a player is off-screen (trailing).
- Independent PWM for each player, indicating individual progress.
- Time-limited mode: race must be completed within a predefined time (e.g., 30 seconds).

---

## 📦 Project Structure

```bash
📁 src/
│   ├── main.c
│   ├── lcd.c
│   ├── pwm.c
│   ├── exti.c
│   └── utils.c
📁 inc/
│   ├── lcd.h
│   ├── pwm.h
│   ├── exti.h
│   └── utils.h
📁 proteus/
│   └── simulation.pdsprj
📄 README.md
📄 report.pdf

