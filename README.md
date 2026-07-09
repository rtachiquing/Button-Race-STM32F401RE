# 🏁 Button Race Game – Final Project (STM32F401RE)

A simple two-player embedded video game for the STM32F401RE microcontroller. Players compete by pressing their buttons as fast as possible to move their animated runner across the LCD screen. The game features character animation, race progress tracking via PWM, external interrupts, and advanced LCD manipulation including display shifting.

---

## 🎮 Project Description

Each player controls a character displayed on their respective line of a 16x2 LCD display. The characters move from left to right as players press their buttons. The faster you press, the faster your character moves. The game uses external interrupts (EXTI) to detect button presses, and timers to calculate press frequency and generate PWM signals proportional to race progress.

<img width="1585" height="1067" alt="image" src="https://github.com/user-attachments/assets/654b9ebd-bc50-47f9-bffe-62bb9b1f5f73" />

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

#### ⭐ Extended Version Alternative 2 – Escape Mode

This alternative introduces a new **Escape Mode** that adds a chasing mechanic to increase the game's difficulty after the player has made significant progress.

Once the player reaches **position 10**, the game automatically enters **Escape Mode**. An enemy character appears at the beginning of the track and starts moving toward the player at a **constant speed**, regardless of the player's actions.

The player continues moving using the push buttons, while the enemy advances periodically using a hardware timer or another timing mechanism implemented on the STM32F401RE.

##### 💀 Defeat Condition

If the enemy reaches the same position as the player (or moves beyond it), the game ends immediately.

The 16×2 LCD must display a blinking message such as: #### **GAME OVER**

The message should blink for several seconds by alternating between the text and a blank screen (or any similar visual effect) to clearly indicate that the player has been caught.

After the animation finishes, the system should return to the main menu or wait for a new game to begin.

##### 🏆 Victory Condition

If the player reaches the finish line before being caught by the enemy, a victory animation must be displayed on the 16×2 LCD.

The animation may include scrolling text, blinking messages, or any other visual effect that clearly indicates the player has successfully escaped.

After the victory sequence, the system should return to the main menu and be ready for a new game.

##### 🎵 Background Chase Music

While **Escape Mode** is active, a passive buzzer must continuously play a simple looping melody generated using PWM and one of the STM32F401RE timers.

The melody should create a feeling of urgency or pursuit and continue playing until one of the following events occurs:

- The player reaches the finish line (Victory).
- The enemy catches the player (Game Over).

Students are free to compose their own melody, provided that it is short, repetitive, and suitable for continuous playback during the chase sequence.

##### ✅ Minimum Requirements

The implementation must include, at minimum, the following features:

- Automatically activate **Escape Mode** when the player reaches position 10.
- Spawn an enemy that moves automatically at a constant speed.
- Allow the player to continue advancing using the push buttons.
- Detect collisions between the player and the enemy.
- Display a blinking **GAME OVER** animation on the 16×2 LCD when the enemy catches the player.
- Display a victory animation if the player reaches the finish line before the enemy.
- Play a continuous chase-themed melody using a passive buzzer during Escape Mode.
- Stop the melody immediately when the game ends, either by victory or defeat.
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

