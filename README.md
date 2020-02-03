
_Organizer's note:_ this project participated in iQuHACK 2020.

---


# Quantum error correction with only two extra qubits in Qiskit

## Dylan Doblar and Finnian Jacobson-Schulte

In this project, we implement the two-extra-qubit [[5,1,3]] quantum error correcting code presented by Chao and Reichardt in [https://arxiv.org/pdf/1705.02329.pdf](https://arxiv.org/pdf/1705.02329.pdf) using Qiskit.  The goal of this project is to demonstrate how QEC schemes can be efficiently implemented in Qiskit and to provide a starting point for others who wish to implement similar schemes.

It is widely recognized that with current quantum devices that QEC is essential for the realization of useful quantum algorithms.  This is due to the relatively high expected error rate in quantum devices due to decoherence and noise in addition to faulty gates and measurements.  

Since current physical devices are extremely limited in number of qubits, it is necessary to have fault tolerant schemes with a relatively low qubit overhead.  The [[5,1,3]] code is the smallest error correcting code, and our implementation achieves fault tolerance using only two extra qubits (seven total).  The scheme uses two flags to which are able to detect and correct gate faults that will cause cascading errors in the data.  We construct four modular syndrome extraction circuits that, when applied in the correct order, marks flag bits that indicate that a single fault will propagate to a higher-weight error.  We can then correct this error and avoid correlated errors in our data.

In our implementation, we first created sub-circuits for syndrome extraction. These sub-circuits also compute the flag bit which will be 1 if propagating errors are detected.  We run our message through each syndrome extraction circuit in order.  At each step, if there is no error detected, we continue to the next syndrome extraction circuit.  If an error is ever detected, we fix the error and return the message.  Note that since this scheme is a [[5,1,3]] scheme, we only fix a single error.
