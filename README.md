# cellular-automata-RNG

This repository contains Python implementations of several cellular automaton models and some basic variations on them. <br/>
Code for generating binary sequences and visualizing cellular automaton evolution using matplotlib is also implemented. <br/>
Finally, the randomness of each automata implemented is tested and compared. 

---

## 📖 **About**
A cellular automaton is a discrete model studied in computational science, consisting of a grid of cells that evolve according to simple rules based on the states of neighboring cells. This project implements automata for Rule 30, Rule 60, and Rule 90.

One key feature of this project is the ability to generate a random binary sequence by extracting the middle column of the evolving cellular automata. This binary sequence has been tested for randomness using the NIST randomness test suite, with results detailed in the [NIST Randomness Test Results](#nist-randomness-test-results) section.

---

## **Rules**
Overall 2 basic rules are tested (Rule 30 and Rule 60) and 4 basic variations (XOR, AND, Alternating Time, Alternating Parity). <br/>
The following are descriptions and visualizations of the variations.

### XOR
Two rules are chosen. The evolutions of both rules are computed independently. Finally, the two resulting 2D grids are XORed to produce the final grid. 

![XOR Visualization](https://github.com/user-attachments/assets/a1c9fe49-523f-47cf-b1a0-74cca0409f05)

### AND
The AND variation computes the element-wise AND between the 2D grids produced by two cellular automata running in parallel. 

![AND Visualization](https://github.com/user-attachments/assets/f699101a-5a11-4a2b-9c8c-4664878d3132)

### Alternating Time
The automaton switches between two rules at each time step, using Rule 30 on even steps and Rule 60 on odd steps (or vice versa). 

![Alternating Time Visualization](https://github.com/user-attachments/assets/f5de580b-2104-4c9f-8b3f-cc0d731bf83f)

### Alternating Parity
For this variation, even-indexed cells follow one rule (e.g., Rule 30) while odd-indexed cells follow another (e.g., Rule 60). This distinction is made at every time step, and cells are updated accordingly. 

![Alternating Parity Visualization](https://github.com/user-attachments/assets/b8e3f3ce-42ad-4bfe-8d37-ac95688a6748)

---

## 📁 **File Outputs**
The binary files generated by `generate_xor_sequence` are stored as `.bin` files in the local directory. The bits in these files correspond to the XOR of the center columns of two cellular automata.

Example file: `xor_30_60.bin`

---

## 📈 **NIST Randomness Test Results**
The randomness of the binary sequences generated from the middle column of the cellular automaton was tested using the NIST randomness test suite. Below is a summary of the results:

### **Test Results**
| **Rule/Test**            | **Frequency** | **Frequency Block** | **Runs** | **Longest Run of Ones** | **Binary Matrix Rank** | **FFT** | **Non-overlapping Template Matching** | **Overlapping Template Matching** | **Maurer's Universal Statistical** | **Linear Complexity** | **Serial** | **Approximate Entropy** | **Cumulative Sums** | **Random Excursions** | **Random Excursions Variant** |
|--------------------------|---------------|---------------------|----------|-------------------------|-------------------------|---------|-------------------------------------|-----------------------------------|-----------------------------------|-----------------------|-----------|-------------------------|---------------------|-----------------------|----------------------------|
| **Rule 30**              | Pass          | Failed              | Failed   | Pass                    | Pass                    | Failed  | Failed                              | Pass                              | Failed                              | Pass                  | Failed    | Failed                  | Failed              | Failed                | Failed                     |
| **Alternating Time**     | Pass          | Pass                | Pass     | Pass                    | Pass                    | Pass    | Pass                                | Pass                              | Pass                                | Pass                  | Pass      | Pass                    | Pass                | Pass                  | Pass                       |
| **Alternating Space**    | Failed        | Pass                | Failed   | Failed                  | Failed                  | Failed  | Failed                              | Failed                            | Failed                              | Failed                | Failed    | Failed                  | Failed              | Failed                | Failed                     |
| **XOR**                  | Pass          | Pass                | Pass     | Pass                    | Pass                    | Pass    | Pass                                | Pass                              | Pass                                | Pass                  | Pass      | Pass                    | Pass                | Pass                  | Pass                       |
| **AND**                  | Failed        | Failed              | Failed   | Failed                  | Pass                    | Failed  | Failed                              | Failed                            | Failed                              | Pass                  | Failed    | Failed                  | Failed              | Failed                | Failed                     |
| **Numpy Random**         | Pass          | Pass                | Pass     | Pass                    | Pass                    | Pass    | Pass                                | Pass                              | Pass                                | Pass                  | Pass      | Pass                    | Pass                | Pass                  | Pass                       |

---

## 🧪 **About the NIST Randomness Tests**
The NIST Statistical Test Suite (STS) is a collection of statistical tests used to evaluate the randomness of binary sequences. Each test examines a specific aspect of randomness, and a failure implies that the binary sequence does not meet the expected statistical properties of randomness for that specific test.

### **Descriptions of the Tests**
1. **Frequency Test**: Verifies whether the number of 1's and 0's in the sequence are roughly equal.
2. **Block Frequency Test**: Similar to the Frequency test but performed on smaller blocks of the sequence.
3. **Runs Test**: Checks for consecutive identical bits ("runs") and verifies if their number matches expected randomness.
4. **Longest Run of Ones**: Analyzes the longest run of consecutive 1's in the sequence.
5. **Binary Matrix Rank**: Tests for linear dependence among fixed-size blocks of the sequence.
6. **Fast Fourier Transform (FFT)**: Detects periodic patterns within the sequence.
7. **Non-overlapping Template Matching**: Counts occurrences of pre-defined bit patterns without overlapping.
8. **Overlapping Template Matching**: Similar to the above but with overlapping allowed.
9. **Maurer's Universal Statistical Test**: Measures the compression of the sequence.
10. **Linear Complexity**: Tests the complexity of the sequence by approximating it with a linear feedback shift register.
11. **Serial Test**: Detects uniformity of overlapping bit sequences.
12. **Approximate Entropy**: Checks for randomness by examining complexity in overlapping bit patterns.
13. **Cumulative Sums**: Evaluates cumulative deviation from zero of the sequence.
14. **Random Excursions**: Analyzes excursions (random walks) of the sequence.
15. **Random Excursions Variant**: Variant of the above, testing deviations based on specific patterns.

### **Implications of Failure**
A test failure implies that the binary sequence exhibits non-random patterns or irregularities for the aspect tested. This does not necessarily mean the entire sequence is non-random, but it highlights weaknesses that may impact its usability in cryptographic or statistical applications.

---

