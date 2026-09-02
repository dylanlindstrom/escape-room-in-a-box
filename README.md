## System Architecture

The system uses an Arduino Mega as the main controller and two Arduino Nano boards to control the individual puzzles.

* **Arduino Mega:** Coordinates the overall system, monitors puzzle completion, communicates with the Nano controllers, and controls the servo mechanisms.
* **Keypad Puzzle Nano:** Handles keypad input, password verification, LED feedback, and lockout logic.
* **Button Puzzle Nano:** Handles button inputs, sequence verification, LED feedback, and puzzle state tracking.
* **I2C Communication:** Allows the Mega and Nano controllers to send activation, completion, and reset signals.
* **Servo Motors:** Control the physical compartment and scissor-lift mechanisms.
* **LEDs:** Provide visual feedback for puzzle states and completion.

The individual puzzle controllers handle their own input and logic, while the Arduino Mega coordinates the progression of the overall system.

## Puzzles

### Keypad Puzzle

The keypad puzzle uses a 4x4 keypad connected to an Arduino Nano. Players enter a four-character password, with the system providing feedback through red and green LEDs.

The puzzle includes:

* Four-character password verification
* Attempt tracking
* Three-attempt lockout
* Password reset functionality
* LED feedback
* I2C communication with the Arduino Mega

### Button Puzzle

The button puzzle uses an Arduino Nano to monitor five push buttons. Players must press the correct buttons in sequence to complete the puzzle.

The firmware uses a state machine to track the player's progress and determine whether each button press is correct or incorrect.

The puzzle includes:

* Sequential button detection
* State-based puzzle logic
* Correct and incorrect input handling
* LED feedback
* Reset functionality
* I2C communication with the Arduino Mega

## Arduino Mega Controller

The Arduino Mega acts as the central controller for the system. It communicates with both puzzle Nano boards and coordinates the progression from one puzzle to the next.

The Mega is responsible for:

* Activating the keypad puzzle
* Activating the button puzzle
* Detecting puzzle completion
* Sending reset signals to the puzzle controllers
* Controlling the compartment servo
* Controlling the scissor-lift servo

## Communication

The system uses I2C communication between the Arduino Mega and the two Nano controllers. Each Nano is assigned its own I2C address so the Mega can communicate with the puzzles independently.

The keypad puzzle uses I2C address **8**, while the button puzzle uses I2C address **9**.

The controllers exchange simple commands to activate and reset the individual puzzles, while the puzzle controllers use output signals to notify the Mega when a puzzle has been completed.

## Technologies Used

### Software

* C++
* Arduino
* I2C communication
* State-based control logic
* Serial debugging

### Hardware

* Arduino Mega
* Arduino Nano
* 4x4 Keypad
* Push buttons
* LED indicators
* Servo motors

### Libraries

* `Wire.h` — I2C communication
* `Servo.h` — Servo motor control
* `Keypad.h` — Keypad input handling

## Repository Structure

```text
escape-room-in-a-box/
├── src/
│   ├── keypad_puzzle/
│   │   └── keypad_puzzle.ino
│   ├── buttons_puzzle/
│   │   └── buttons_puzzle.ino
│   └── mega_controller/
│       └── mega_controller.ino
├── .gitignore
├── LICENSE
└── README.md
```

### Source Files

* **`keypad_puzzle.ino`** — Controls the keypad puzzle, password validation, lockout logic, LED feedback, and I2C communication.
* **`buttons_puzzle.ino`** — Controls the sequential button puzzle, state machine, LED feedback, and I2C communication.
* **`mega_controller.ino`** — Coordinates the puzzle controllers and controls the servo mechanisms.

## Debugging and Integration

Because the system uses multiple microcontrollers, communication and integration between the boards were important parts of the project.

The puzzle logic was separated across the Nano controllers so that each puzzle could operate independently while the Mega handled overall system coordination. Serial output was also used throughout the firmware to monitor puzzle states, inputs, communication, and system events during development and debugging.

## Project Result

The completed system integrated multiple microcontrollers, interactive puzzles, I2C communication, LED feedback, and servo-controlled mechanisms into a single portable embedded system.

The project placed **2nd in the final project competition/demo**.

## Future Improvements

Potential improvements include:

* Replacing blocking `delay()` calls with non-blocking timing using `millis()`
* Adding more robust I2C error handling
* Improving button input debouncing
* Further modularizing the firmware
* Adding additional interchangeable puzzles
* Adding detailed hardware wiring and system diagrams
