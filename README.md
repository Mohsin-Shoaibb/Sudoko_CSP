## Sudoku Solver (CSP-Based)

This repository contains a high-performance **Sudoku Solver** implemented in Python. It approaches Sudoku as a **Constraint Satisfaction Problem (CSP)**, utilizing advanced search and inference techniques to solve puzzles ranging from easy to "extreme" difficulty.

---

### 🚀 Features

* **AC-3 Algorithm:** Implements Arc Consistency to prune the search space by removing impossible values from cell domains before and during search.
* **Backtracking Search:** Uses a depth-first search strategy to find the valid configuration.
* **MRV Heuristic:** Employs the **Minimum Remaining Values** heuristic to select the next cell to branch on, significantly reducing the branching factor.
* **Forward Checking:** Integrates look-ahead consistency checks to detect failures early.
* **Customizable Input:** Reads puzzles from simple text files.

---

### 🧠 How It Works

The solver treats the 9x9 grid as a graph of 81 variables. Each variable has a domain of $\{1, \dots, 9\}$. The constraints are defined by the standard Sudoku rules:
1.  Each row must contain unique digits.
2.  Each column must contain unique digits.
3.  Each 3x3 sub-grid must contain unique digits.

The script uses **Arc Consistency ($AC-3$)** to ensure that for every pair of related cells $(X_i, X_j)$, every value in the domain of $X_i$ has at least one possible value in $X_j$ that satisfies the constraints.

---

### 🛠️ Installation & Usage

#### Prerequisites
* Python 3.x

#### Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/sudoku-csp-solver.git
   cd sudoku-csp-solver
   ```
2. Create a puzzle file (e.g., `medium.txt`). Use `0` to represent empty cells:
   ```text
   003020600
   900305001
   001806400
   008102900
   700000008
   006708200
   002609500
   800203009
   005010300
   ```

#### Running the Solver
Run the script by passing your puzzle file via the `main` execution:
```bash
python solver.py
```
*(Note: Ensure the filename in `if __name__ == "__main__":` matches your text file, or modify it to accept sys.args)*.

---

### 📊 Code Structure

* `get_neighbors(i)`: Pre-calculates the constraints for every cell (row, column, and box peers).
* `revise(domains, xi, xj)`: The core inference function that trims domains.
* `ac3(domains, neighbors)`: Maintains arc consistency across the entire board.
* `solve_backtracking(domains, neighbors)`: The recursive search function that guesses values and backtracks upon conflict.
* `print_board(domains)`: A utility to output the solved grid in a human-readable 9x9 format.

---

### 📝 Example Output

```text
4 8 3 | 9 2 1 | 6 5 7
9 6 7 | 3 4 5 | 8 2 1
2 5 1 | 8 7 6 | 4 9 3
---------------------
5 4 8 | 1 3 2 | 9 7 6
7 2 9 | 5 6 4 | 1 3 8
1 3 6 | 7 9 8 | 2 4 5
---------------------
3 7 2 | 6 8 9 | 5 1 4
8 1 4 | 2 5 3 | 7 6 9
6 9 5 | 4 1 7 | 3 8 2
```

---

### ⚖️ License
This project is open-source and available under the MIT License.
