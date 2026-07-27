<p align="right">
  <b>English</b> | <a href="README.fa.md">فارسی</a>
</p>

---
# Space Cow Transport — MIT 6.00.2x PSet 1

> Algorithmic optimization for space livestock transport using Greedy and Brute Force strategies.

---

## Table of Contents
- [Description](#description)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Installation / How to Run](#installation--how-to-run)
- [Project Structure](#project-structure)
- [Design Choices / Challenges](#design-choices--challenges)
- [Screenshots](#screenshots)
- [Credits / Acknowledgements](#credits--acknowledgements)
- [License](#license)

---

## Description

This project addresses an optimization problem based on MIT 6.00.2x (Introduction to Computational Thinking and Data Science). A colony of alien bioengineers needs to transport mutant cows from Earth back to their home planet. Given a spaceship with a strict weight capacity per trip, the objective is to minimize the total number of trips required to transport all cows.

The problem is a variant of the **Bin Packing Problem** (an NP-hard problem). This repository implements two distinct computational strategies to solve it:
1. A **Greedy Heuristic Algorithm** that trades guaranteed global optimality for fast execution.
2. A **Brute Force Algorithm** that searches through set partitions to guarantee the absolute minimal number of trips.

---

## Features

* **Greedy Transport Strategy:** Always picks the heaviest available cow that fits within the remaining spaceship weight limit for each trip.
* **Brute Force Transport Strategy:** Enumerates all valid set partitions of cows, identifying the globally minimal trip allocation.
* **Performance Benchmarking:** Includes a comparison utility measuring execution time (`time.time()`) and solution quality (trip count) between both algorithms.
* **Immutable Data Handling:** Ensures input cow data dictionaries remain unmutated throughout processing.

---

## Technologies Used

* **Python 3.x**
* **Standard Python Modules:** `time`

---

## Installation / How to Run

### Prerequisites
* Python 3.6 or higher installed on your system.

### Steps

1. **Clone the Repository:**
   ```bash
   git clone [https://github.com/mamadlari/MIT-6.00.2x.git](https://github.com/mamadlari/MIT-6.00.2x.git)
   cd MIT-6.00.2x/Pset1

```

2. **Ensure File Alignment:**
Verify that `ps1.py`, `ps1_partition.py`, and `ps1_cow_data.txt` are all located in the same directory.
3. **Run the Script:**
```bash
python ps1.py

```



---

## Project Structure

```text
Pset1/
│
├── ps1.py              # Main implementation file containing algorithms and benchmarking
├── ps1_partition.py    # Helper generator function for set partitions
└── ps1_cow_data.txt    # Input dataset (Cow Name, Weight in tons)

```

---

## Design Choices / Challenges

### 1. Greedy Choice Heuristic vs. Global Optimality

The greedy algorithm sorts the cow inventory by weight in descending order. On each trip, it repeatedly fits the heaviest remaining cow into the current ship payload.

* **Trade-off:** This approach runs efficiently with low computational complexity. However, because local greedy choices do not account for future space utilization, it does not guarantee the theoretical minimum number of trips.

### 2. Set Partitioning in Brute Force Search

To guarantee an optimal solution via brute force, the algorithm generates all possible set partitions using `get_partitions()`.

* **Execution Strategy:** The partition generator yields trip combinations ordered by the number of subsets (trips). The algorithm tests each partition sequentially for weight constraint compliance. The first valid partition encountered is guaranteed to have the minimal number of trips, allowing an early return to avoid unnecessary computational overhead.

### 3. Data Integrity & State Management

Both algorithms operate without mutating the underlying input dictionary (`cows`). Working on local copies and key list abstractions prevents side-effects across repeated benchmark runs.

---

## Screenshots

> *Placeholder for terminal output screenshot comparing Greedy vs. Brute Force execution timing and trip results.*

```text
+-----------------------------------------------------------------------+
|  Greedy Transport Results:                                            |
|  - Number of trips: 4                                                 |
|  - Execution Time: 0.0001s                                            |
|                                                                       |
|  Brute Force Transport Results:                                       |
|  - Number of trips: 3                                                 |
|  - Execution Time: 0.4521s                                            |
+-----------------------------------------------------------------------+

```

---

## Credits / Acknowledgements

* Problem set concept and starter code provided by **MIT 6.00.2x** (*Introduction to Computational Thinking and Data Science*), available via edX.

---

## License

This project is open-source and intended for educational and portfolio demonstration purposes.

```

```