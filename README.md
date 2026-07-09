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

#### ⭐ Versión Extendida Alternativa 2 – Escape

En esta versión extendida, el juego incorpora una nueva mecánica de persecución que incrementa la dificultad una vez que el jugador ha avanzado lo suficiente en el recorrido.

Cuando el jugador alcance la casilla 10, el juego entrará automáticamente en el Modo Persecución. A partir de ese momento aparecerá un enemigo en la primera casilla del tablero, el cual avanzará automáticamente hacia el jugador a una velocidad constante, independientemente de las acciones del usuario.

El jugador continuará desplazándose mediante los botones del sistema, mientras que el enemigo realizará movimientos periódicos utilizando una base de tiempo implementada con un temporizador del microcontrolador.

Condición de derrota

Si el enemigo alcanza la misma casilla que ocupa el jugador (o una posición superior), la partida finalizará inmediatamente.

El LCD de 16×2 deberá mostrar un mensaje de:

#### *** GAME OVER ***

Este mensaje deberá presentarse mediante un efecto de parpadeo (encendiendo y apagando el texto o alternándolo con una pantalla en blanco) durante algunos segundos para indicar claramente la derrota del jugador.

Al finalizar la animación, el sistema deberá regresar al menú principal o quedar listo para iniciar una nueva partida.

Condición de victoria

Si el jugador consigue llegar a la casilla final antes de ser alcanzado por el enemigo, el juego deberá mostrar una animación de victoria en el LCD de 16×2.

La animación puede consistir en el desplazamiento del mensaje de felicitación, un efecto de parpadeo, o cualquier otra secuencia que indique claramente que el jugador ha ganado la partida.

Una vez concluida la animación, el sistema volverá al menú principal para permitir el inicio de un nuevo juego.

Melodía durante la persecución

Mientras el juego permanezca en el Modo Persecución, un buzzer pasivo deberá reproducir continuamente una melodía sencilla generada mediante PWM y un temporizador del STM32F401RE.

La melodía deberá transmitir una sensación de tensión o persecución y reproducirse en un ciclo continuo hasta que ocurra una de las siguientes condiciones:

El jugador llegue a la meta (victoria).
El enemigo alcance al jugador (derrota).

La secuencia de notas puede ser diseñada libremente por el estudiante, siempre que mantenga una duración breve y pueda repetirse de forma continua durante toda la fase de persecución.

#### Requisitos mínimos

La implementación deberá cumplir, como mínimo, con los siguientes puntos:

- Activar el Modo Persecución cuando el jugador alcance la casilla 10.
- Generar un enemigo que avance automáticamente a una velocidad constante.
- Permitir que el jugador continúe desplazándose mediante los botones del sistema.
- Detectar la colisión entre el jugador y el enemigo.
- Mostrar una animación de GAME OVER en el LCD de 16×2 cuando el enemigo alcance al jugador.
- Mostrar una animación de victoria cuando el jugador llegue a la meta antes que el enemigo.
- Reproducir una melodía de persecución utilizando un buzzer pasivo durante toda la fase de persecución.
- Detener la melodía cuando el juego finalice, ya sea por victoria o por derrota.
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

