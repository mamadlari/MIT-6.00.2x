<p align="right">
  <b>English</b> | <a href="README.fa.md">فارسی</a>
</p>

---
# iRobot Roomba Vacuum Simulation (MIT 6.00.2x)

A discrete-time simulation engine in Python that models autonomous vacuum cleaner robots operating inside rectangular rooms to evaluate and compare movement strategies and cleaning efficiency.

---

## Table of Contents

* [Description](https://www.google.com/search?q=%23description)
* [Features](https://www.google.com/search?q=%23features)
* [Technologies Used](https://www.google.com/search?q=%23technologies-used)
* [Project Structure](https://www.google.com/search?q=%23project-structure)
* [Installation & Usage](https://www.google.com/search?q=%23installation--usage)
* [Design Choices & Technical Challenges](https://www.google.com/search?q=%23design-choices--technical-challenges)
* [Screenshots](https://www.google.com/search?q=%23screenshots)
* [Acknowledgements](https://www.google.com/search?q=%23acknowledgements)
* [License](https://www.google.com/search?q=%23license)

---

## Description

This project simulates autonomous cleaning robots (modeled after iRobot Roombas) operating in rectangular rooms. The primary objective is to evaluate how different movement strategies impact the total time required to clean a target percentage of a room.

Through Monte Carlo simulations across multiple independent trials, the engine computes mean time-steps required under varying configurations (e.g., varying robot counts, movement patterns, and room dimensions/aspect ratios).

---

## Features

* **Discrete-Time Simulation Engine**: Calculates average cleaning time across $N$ trials for specified target coverage thresholds (`min_coverage`).
* **Object-Oriented Architecture**: Utilizes class inheritance to decouple room models, position calculations, and movement strategy implementations.
* **Polymorphic Movement Strategies**:
* `StandardRobot`: Moves in a straight path until colliding with a wall, then selects a new random direction.
* `RandomWalkRobot`: Changes direction randomly at every single time-step.


* **Multi-Robot Synchronization**: Supports $N$ robots operating concurrently inside the same physical space.
* **Graphical Visualization**: Integrated Tkinter-based animation rendering real-time tile state updates (gray to white).
* **Data Plotting**: Uses `matplotlib` / `pylab` to generate comparative performance plots (Time vs. Robot Count and Time vs. Room Aspect Ratio).

---

## Technologies Used

* **Python 3.x**
* **Matplotlib / PyLab**: For generating simulation analytics plots.
* **Tkinter**: (Python standard library) For live simulation visualization.
* **Math & Random**: (Python standard modules) For trigonometric position updates and uniform random distributions.

---

## Project Structure

```text
.
├── ps2.py              # Main logic: Position, Room, Robot classes, simulation loops, and plotting
├── ps2_visualize.py    # GUI animation module utilizing Tkinter
└── README.md           # Project documentation

```

---

## Installation & Usage

### Prerequisites

* Python 3.x installed on your system.
* Note: Standard libraries `math`, `random`, and `tkinter` come pre-installed with standard Python distributions.

### 1. Installation

Clone the repository and install `matplotlib`:

```bash
git clone https://github.com/mamadlari/MIT-6.00.2x.tree/main/Pset2
cd Pset2
pip install matplotlib

```

### 2. Configuration & Execution

To execute the project, open `ps2.py` and adjust the uncommented function calls at the bottom of the file depending on the desired mode:

* **To output simulation mean metrics in the console:**
Uncomment the relevant `print(runSimulation(...))` calls.
* **To render analytics plots:**
Uncomment `showPlot1()` or `showPlot2()` calls at the bottom of `ps2.py`.
* **To enable real-time animation:**
Uncomment the visualization lines inside `runSimulation()`:
```python
anim = ps2_visualize.RobotVisualization(num_robots, width, height)
# inside the simulation loop:
anim.update(room, robots)
# at trial completion:
anim.done()

```



Run the script using:

```bash
python ps2.py

```

---

## Design Choices & Technical Challenges

### 1. Simultaneous Discrete-Time Movement

* **Challenge**: Modeling $N$ robots moving concurrently within a single discrete time-step without timing desynchronization.
* **Solution**: In every clock tick, the simulation loop iterates over all robot instances, invoking `updatePositionAndClean()`. The global time-step counter increments only after every active robot has processed its move and updated the room state.

### 2. Shared Room State & Memory Management

* **Challenge**: Ensuring all $N$ active robots update a unified room representation rather than local copies.
* **Solution**: Passed a single `RectangularRoom` instance reference to all robot constructors during initialization. Mutating tile cleanliness (`self.cleaned_tiles`) within the shared instance guarantees real-time state synchronization across all robots.

### 3. Inheritance & Strategy Pattern

* **Challenge**: Allowing seamlessly interchangeable movement strategies within the simulation loop without modifying the runner function.
* **Solution**: Abstracted general robot properties (position, speed, room reference) into a base `Robot` class. Derived `StandardRobot` and `RandomWalkRobot` classes override `updatePositionAndClean()`, exposing a identical polymorphic interface to `runSimulation(..., robot_type)`.

---

## Screenshots
> *output for runSimulation(1, 1.0, 20, 20, 1, 30, RandomWalkRobot) result.*

```bash
Average number of time steps for RandomWalkRobot: 8573.766666666666

```

### Real-Time Simulation
![Robot Simulation(standard)](assets/simulation.png)
### Performance Benchmarks

| Time vs. Number of Robots | Time vs. Room Aspect Ratio |
| :---: | :---: |
| ![Plot 1](assets/plot1.png) | ![Plot 2](assets/plot2.png) |

---

## Acknowledgements

* **MIT 6.00.2x: Introduction to Computational Thinking and Data Science** (Massachusetts Institute of Technology / edX) for providing the problem set specifications and starter framework.

---

## License

This project is open-source and available under the [MIT License](https://www.google.com/search?q=LICENSE).