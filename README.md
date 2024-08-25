# Hamming Error Detection and Correction (Single Bit)

This project demonstrates an error detection and correction technique using Hamming Code, specifically designed to detect both single-bit and double-bit errors when binary data is transmitted from one end to another. It is a type of forward error correction coding that eliminates the need for retransmission when data corruption is detected. In this design, a Hamming code for single-bit error detection and correction is implemented using Verilog HDL.

## Key Terms

1. **Codeword (n)**: The complete set of bits, including both data and redundant bits, that is transmitted.
2. **Redundant / Parity bits (k)**: Extra bits added to the data to enable error detection and correction.
3. **Dataword (n-k)**: The original data bits being transmitted, excluding the redundant bits.
4. **Number of correction bits (t)**: The number of bits that can be corrected by the Hamming Code.

In this design, we use the parameters (n, k, t) = (12, 4, 1) defined as follows:
- **Dataword**: {m<sub>3</sub>, m<sub>5</sub>, m<sub>6</sub>, m<sub>7</sub>, m<sub>9</sub>, m<sub>10</sub>, m<sub>11</sub>, m<sub>12</sub>}
- **Parity bits**: {p<sub>1</sub>, p<sub>2</sub>, p<sub>4</sub>, p<sub>8</sub>}
- **Codeword**: {p<sub>1</sub>, p<sub>2</sub>, m<sub>3</sub>, p<sub>4</sub>, m<sub>5</sub>, m<sub>6</sub>, m<sub>7</sub>, p<sub>8</sub>, m<sub>9</sub>, m<sub>10</sub>, m<sub>11</sub>, m<sub>12</sub>}

## Encoder

The encoder module, at the transmitting side, generates parity bits for encoding the incoming data into a codeword. The dataword becomes more robust to errors when redundant bits are added. Each parity bit is calculated using the exclusive OR operation (XOR) on specific data bits, based on the positions determined by powers of two.

For this implementation:

- **p<sub>1</sub>** = m<sub>3</sub> ⊕ m<sub>5</sub> ⊕ m<sub>7</sub> ⊕ m<sub>9</sub> ⊕ m<sub>10</sub> ⊕ m<sub>11</sub>
- **p<sub>2</sub>** = m<sub>3</sub> ⊕ m<sub>6</sub> ⊕ m<sub>7</sub> ⊕ m<sub>10</sub> ⊕ m<sub>11</sub>
- **p<sub>4</sub>** = m<sub>5</sub> ⊕ m<sub>6</sub> ⊕ m<sub>7</sub> ⊕ m<sub>12</sub>
- **p<sub>8</sub>** = m<sub>9</sub> ⊕ m<sub>10</sub> ⊕ m<sub>11</sub> ⊕ m<sub>12</sub>

## Decoder

The decoder module at the receiving side is responsible for detecting the position of a bit that might be corrupted during transmission. To locate the corrupted bit, the decoder recalculates the parity bits using the received data and compares them with the transmitted parity bits.

For error location, we define:

- **C<sub>1</sub>** = p<sub>1</sub> ⊕ m<sub>3</sub> ⊕ m<sub>5</sub> ⊕ m<sub>7</sub> ⊕ m<sub>9</sub> ⊕ m<sub>11</sub>
- **C<sub>2</sub>** = p<sub>2</sub> ⊕ m<sub>3</sub> ⊕ m<sub>6</sub> ⊕ m<sub>7</sub> ⊕ m<sub>10</sub> ⊕ m<sub>11</sub>
- **C<sub>3</sub>** = p<sub>4</sub> ⊕ m<sub>5</sub> ⊕ m<sub>6</sub> ⊕ m<sub>7</sub> ⊕ m<sub>12</sub>
- **C<sub>4</sub>** = p<sub>8</sub> ⊕ m<sub>9</sub> ⊕ m<sub>10</sub> ⊕ m<sub>11</sub> ⊕ m<sub>12</sub>

The final error location is determined by concatenating these bits into a single number: **C = {C<sub>4</sub>, C<sub>3</sub>, C<sub>2</sub>, C<sub>1</sub>}**.

## Correction

Once the position of the corrupted bit is identified, the bit can be corrected by simply flipping (complementing) its value, thus restoring the original data.

## Simulation

The design has been simulated using **Vivado 2016.2**. The simulation results confirm that the design successfully detects and corrects single-bit errors.

### Simulation Results:

- **Encoding Simulation:**

  ![Encoding Simulation](./Images/encoding_simulation_graph.PNG)

- **Decoding and Correction Simulation:**

  ![Decoding Simulation](./Images/decoding_simulation_graph.PNG)

## Conclusion

This project successfully implements Hamming Code for single-bit error detection and correction using Verilog HDL. It demonstrates an effective method for ensuring data integrity in digital communication systems where reliability is essential.

---

Thank you for reading! Have a nice day! 😄
