# Notes on the Project

Requirements and suggestions from the Professor:
- Notebook code should be well commented
- Presentation slides should take 10 minutes to present
- Pay particular attention on the obtained results and do not present the protocol from scratch in the slides
- Send all the project files int the Teams channel 4-5 days before the presentation


---

[Here](https://en.wikipedia.org/wiki/Quantum_correlation) can be found the formula that I used for the computation of the expected value (the Quantum Correlation), that is:

$$\frac{N_{++} - N_{+-} - N_{-+} + N_{--}}{N_{total}}$$

where $N_{total}$ is, in general, equal to $N_{++} + N_{+-} + N_{-+} + N_{--}$.

Theory related to the [CHSH inequality](https://en.wikipedia.org/wiki/CHSH_inequality)

Bound for the CHSH inequality, [Tsirelson's bound](https://en.wikipedia.org/wiki/Tsirelson%27s_bound)

The notation $[A_i, B_j] = 0$ refers to the **commutator** of two operators $A_i$ and $B_j$, defined as:

$$[A_i, B_j] = A_i B_j - B_j A_i$$

When $[A_i, B_j] = 0$, it means that the operators $A_i$ and $B_j$ **commute**. In other words:

$$A_i B_j = B_j A_i$$

### Physical Meaning in the Context of CHSH Inequality
In quantum mechanics, the commutator being zero implies that the two observables $A_i$ and $B_j$ can be measured simultaneously without affecting each other. This is crucial in the context of the CHSH inequality because:

- $A_i$ represents Alice's measurement observable.
- $B_j$ represents Bob's measurement observable.

The condition $[A_i, B_j] = 0$ ensures that the measurements performed by Alice and Bob do not interfere with each other. This is a necessary requirement for the CHSH inequality to be properly defined, as it assumes that the correlations between measurements of $A_i$ and $B_j$ can be meaningfully compared.

### Why Do Alice and Bob's Observables Commute?
Alice and Bob's observables typically act on **different qubits** in an entangled system. Since they operate on separate subsystems, their operators commute by construction. For example, if $A_i$ acts on Alice's qubit and $B_j$ acts on Bob's qubit, their actions are independent, and therefore:

$$[A_i, B_j] = 0$$

This ensures that measurements by Alice and Bob can be analyzed together in the CHSH framework.