
Hamming Code Error Detection and Correction (Single Bit) - Verilog HDL
Overview
This project implements Hamming Code for error detection and correction using Verilog HDL. Hamming Code is a forward error correction coding method capable of detecting both single and double-bit errors while correcting single-bit errors in transmitted binary data. This design improves data reliability without requiring data retransmission, making it ideal for applications where real-time communication and data integrity are critical.

Key Concepts
Codeword (n): The full set of bits sent over the transmission medium, which includes both data and parity bits.
Redundant / Parity bits (k): Extra bits added to the data to enable error detection and correction.
Dataword (n-k): The original data bits being transmitted, excluding the parity bits.
Number of correction bits (t): The number of bits that can be corrected by the Hamming Code.
In this project, the parameters are set as follows:

(n, k, t) = (12, 4, 1)
Dataword = {m3, m5, m6, m7, m9, m10, m11, m12}
Parity bits = {p1, p2, p4, p8}
Codeword = {p1, p2, m3, p4, m5, m6, m7, p8, m9, m10, m11, m12}
Design Components
1. Encoder
The encoder module generates parity bits and forms a codeword from the incoming dataword at the transmitting end. The parity bits are calculated using the XOR operation on specific data bits based on their positions, following the Hamming code method:

p1 = m3 ⊕ m5 ⊕ m7 ⊕ m9 ⊕ m10 ⊕ m11
p2 = m3 ⊕ m6 ⊕ m7 ⊕ m10 ⊕ m11
p4 = m5 ⊕ m6 ⊕ m7 ⊕ m12
p8 = m9 ⊕ m10 ⊕ m11 ⊕ m12
2. Decoder
The decoder module identifies the position of any bit that might have been corrupted during transmission. It recalculates parity bits using the received data bits and the parity bits and then compares them:

C1 = p1 ⊕ m3 ⊕ m5 ⊕ m7 ⊕ m9 ⊕ m11
C2 = p2 ⊕ m3 ⊕ m6 ⊕ m7 ⊕ m10 ⊕ m11
C3 = p4 ⊕ m5 ⊕ m6 ⊕ m7 ⊕ m12
C4 = p8 ⊕ m9 ⊕ m10 ⊕ m11 ⊕ m12
The results are combined to form C = {C4, C3, C2, C1}, indicating the exact position of any single-bit error.

3. Correction
After locating the corrupted bit using C, the bit is corrected by flipping its value, thereby restoring the data integrity.

Simulation
This design has been simulated using Vivado 2016.2. The simulation waveforms verify that the design accurately detects and corrects single-bit errors, ensuring data integrity.

Getting Started
Install Vivado 2016.2 or a compatible version.
Create a new project in Vivado and add the provided Verilog source files.
Set up the simulation environment according to the project requirements.
Run the simulation to observe the error detection and correction behavior.
Conclusion
This project successfully implements Hamming Code for single-bit error detection and correction using Verilog HDL. It demonstrates an effective method for enhancing data integrity in digital communication systems, especially where reliability is paramount.

License
This project is licensed under the MIT License.
