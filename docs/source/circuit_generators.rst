Circuit Generators
==================

Functions to setup common `quantum
circuits <https://qiskit.org/documentation/stubs/qiskit.circuit.QuantumCircuit.html>`__
in Qiskit for a given number of qubits.

Functions
---------

All functions take the number of qubits as argument, and return the
corresponding Qiskit circuit. One can then use the Qiskit backend to
transpile the circuit for a specific quantum device.

.. code:: python

   from quantum_gates.circuit_generators import (
       hadamard_reverse_QFT_circ, 
       GHZ_circ, 
       QFT_circ
       QAOA_circ
   )

   nqubit = 2
   circuit = hadamard_reverse_QFT_circ(nqubit=2)
   circ.draw('mpl')

hadamard_reverse_QFT_circ
~~~~~~~~~~~~~~~~~~~~~~~~~

This generators creates the circuit consisting of Hadamard gates,
followed by the inverse of the Quantum Fourrier Transform. A useful
property of the circuit is that it maps the all 0 state to the equal
superposition of all states, and back to the 0 state. As we know the
ideal result, we can calculate fidelity metrics easily.

GHZ_circ
~~~~~~~~

The generated circuit generates the `Greenberger–Horne–Zeilinger (GHZ)
state <https://en.wikipedia.org/wiki/Greenberger%E2%80%93Horne%E2%80%93Zeilinger_state>`__
from the zero state. The GHZ is maximally entangled and implemented by
applying a Hadamard gate on the first qubit, and then subsequently
applying CNOT gates with source i, target i+1, for i = 0, …, nqubit - 2.

QFT_circ
~~~~~~~~

Generates the Quantum Fourrier Transform.

QAOA_circ
~~~~~~~~~

Generates a circuit for a Quantum Approximate Optimization Algorithm.
