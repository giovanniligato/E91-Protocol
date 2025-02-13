# E91 Quantum Key Distribution Protocol
![E91 Protocol](Slides/E91%20Protocol%20[JPG]/Diapositiva1.JPG)

## Introduction
Securely sharing cryptographic keys over insecure channels represents a fundamental challenge in modern cryptography. Traditional key distribution methods depend on *computational complexity*, a premise that is increasingly vulnerable in light of future advances in computational power.

The **E91 protocol**, proposed by Artur Ekert in 1991, exploits the principles of *quantum entanglement* and the *no-cloning theorem* to establish an infinitely-secure key distribution mechanism. By leveraging the *CHSH inequality* and *Bell’s theorem*—which demonstrates that quantum mechanics cannot be explained by any local hidden variable theory and thereby confirms the existence of quantum entanglement—the E91 protocol guarantees that any eavesdropping attempt is detectable, rendering the key exchange process inherently secure.

## Background

### The Problem
Classical cryptographic systems rely on the assumed intractability of certain mathematical problems (e.g., factoring large numbers in RSA). However, quantum computers have the potential to efficiently solve these problems using algorithms such as *Shor’s algorithm*. This vulnerability necessitates the development of cryptographic methods that remain secure even in the presence of quantum computational capabilities.

### The Solution
The *E91 QKD protocol* utilizes pairs of entangled photons to securely distribute cryptographic keys between parties. The fundamental idea is that measurements on entangled qubits produce correlations that defy classical explanation, thereby ensuring security against eavesdropping. The integrity of the key is confirmed through the application of *Bell’s theorem*—and, in particular, the *CHSH inequality*—which is used to detect any deviations from the expected quantum correlations.

## Scenarios Considered
The implementation and simulation of the E91 protocol were analyzed under three primary scenarios:

1. **Ideal Conditions**: The communication channel is assumed to be free of errors, and no eavesdropping occurs.
2. **Channel Errors**: The quantum channel experiences errors (noise), but no eavesdropping is present.
3. **Eavesdropping Scenario**: An adversary, *Eve*, conducts eavesdropping attacks while the channel itself remains error-free.

## The Specialized Circuit for Generating Werner States
The following circuit is employed to generate entangled photon pairs. At the bottom of the slide, the corresponding density matrix representation of the circuit’s output is provided, which illustrates the state of the system after the application of the circuit.

![E91 Protocol](Slides/E91%20Protocol%20[JPG]/Diapositiva4.JPG)

## 1. Ideal Conditions
In the ideal scenario, the circuit is configured with a parameter setting of $\theta = \pi$. This configuration yields the pure entangled state:
$$ \psi^- = \frac{1}{\sqrt{2}}\left(|01\rangle - |10\rangle\right) $$
This state represents the maximal entanglement between the two qubits, ensuring optimal key generation performance and the highest possible violation of the CHSH inequality.

## 2. Channel Errors
Channel errors are simulated by employing the same generalized circuit with $\theta$ values in the range:
$$ 0 \leq \theta < \pi $$
By varying $\theta$, the circuit produces Werner states that represent mixed quantum states. As $\theta$ deviates from the ideal value, the output state becomes increasingly depolarized, simulating the effect of noise in the quantum channel. This degradation in entanglement is reflected in both a decrease in the CHSH correlation value and an increase in the mismatch ratio between the keys generated by the communicating parties.

## 3. Eavesdropping (Eve’s Attack)
In the eavesdropping scenario, the adversary (Eve) takes control of the entanglement generation process. Instead of distributing entangled photon pairs, Eve sends, with a probability of $\frac{1}{2}$, the separable states $|00\rangle$ or $|11\rangle$ to Alice and Bob. This substitution undermines the quantum correlations, thereby reducing the CHSH correlation value. As a consequence, the legitimate parties can detect the presence of an eavesdropper and abort the protocol to maintain security.

## Protocol Details

The observables used by Alice and Bob in their measurements are defined as follows:

**Alice's Observables:**
- $A_0 = Z$
- $A_1 = X$
- $A_2 = \frac{Z + X}{\sqrt{2}}$

**Bob's Observables:**
- $B_0 = Z$
- $B_1 = \frac{Z - X}{\sqrt{2}}$
- $B_2 = \frac{Z + X}{\sqrt{2}}$

The CHSH correlation value is computed using the formula:
$$ S = \left| \langle A_0 B_2 \rangle + \langle A_0 B_1 \rangle + \langle A_1 B_2 \rangle - \langle A_1 B_1 \rangle \right| $$
This value serves as an indicator of the degree of entanglement present in the system, with a higher value corresponding to stronger quantum correlations.

## The Metrics to Evaluate

The primary metrics used for evaluation are:

- **CHSH Correlation Value (S):** Quantifies the strength of the quantum entanglement. A value approaching the theoretical maximum of $2\sqrt{2}$ indicates a high degree of entanglement.
- **Mismatch Ratio (R$_m$):** Represents the fraction of mismatched bits between the keys generated by Alice and Bob. A lower mismatch ratio corresponds to a more reliable key exchange.

These quantities are analyzed as functions of $\theta$ (or equivalently, the Werner parameter) to assess the impact of channel errors and eavesdropping on the key distribution process.

## Results

### 1. Ideal Conditions
Under ideal conditions, the protocol achieves the theoretical maximum CHSH value of $2\sqrt{2}$, and the mismatch ratio is effectively 0, indicating perfect key agreement between the communicating parties.

### 2. Channel Errors
As the parameter $\theta$ approaches 0—resulting in a completely mixed state—the CHSH value decreases while the mismatch ratio increases, reaching values as high as 0.5. This degradation demonstrates the adverse effect of noise on the quantum channel.

### 3. Eavesdropping Scenario
In the presence of an eavesdropper, the CHSH correlation value does not reach the quantum threshold of $2\sqrt{2}$. Instead, it remains significantly lower, typically within the range of 1.0 to 1.5. This reduction is a clear indicator of tampering, enabling Alice and Bob to detect the anomaly and abort the protocol before any secure key is generated.

## Conclusion
The **E91 QKD protocol** offers a highly secure method for key distribution by leveraging the unique properties of quantum entanglement. The experimental and simulated results confirm that:
- **Ideal conditions** yield optimal security and reliable key generation.
- **Channel errors** lead to a degradation of entanglement, thereby necessitating the use of error correction techniques.
- **Eavesdropping** is effectively detected through a significant reduction in the CHSH correlation value, prompting the aborting of the key exchange process.

## References and Tools
![References and Tools](Slides/E91%20Protocol%20[JPG]/Diapositiva30.JPG)