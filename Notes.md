# 1. Notes on the Project

## 1.1. Suggestions from the Professor

Requirements and suggestions from the Professor:

- Notebook code should be well commented;
- Presentation slides should take 10 minutes to present;
- Pay particular attention on the obtained results and do not present the protocol from scratch in the slides;
- Send all the project files in the Teams channel 4-5 days before the presentation.


## 1.2. Miscellaneous

### 1.2.1. Expected Value (Quantum Correlation)

For the computation of the expected value (Quantum Correlation), the formula used is given in this Wikipedia page: [Quantum correlation](https://en.wikipedia.org/wiki/Quantum_correlation).

$$ \frac{N_{++} - N_{+-} - N_{-+} + N_{--}}{N_{\text{total}}}$$

where $N_{\text{total}} = N_{++} + N_{+-} + N_{-+} + N_{--}$.

### 1.2.2. CHSH Inequality

Additional theoretical details can be found in the context of the [CHSH inequality](https://en.wikipedia.org/wiki/CHSH_inequality) and its upper limit, [Tsirelson's bound](https://en.wikipedia.org/wiki/Tsirelson%27s_bound).

### 1.2.3. Commutator

The commutator of two operators $A_i$ and $B_j$ is defined as:

$$ [A_i, B_j] = A_i B_j - B_j A_i. $$

When $[A_i, B_j] = 0$, it indicates that the operators commute:

$$ A_i B_j = B_j A_i. $$

**Physical Interpretation in the CHSH Inequality Context**

In quantum mechanics, a zero commutator signifies that the observables $A_i$ and $B_j$ can be measured simultaneously without interference. In the CHSH framework:
- $A_i$ denotes Alice’s measurement observable.
- $B_j$ denotes Bob’s measurement observable.

Since these operators typically act on different qubits in an entangled system, they commute by construction, ensuring that the measurements can be meaningfully compared in the CHSH analysis.