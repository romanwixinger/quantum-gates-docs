Welcome to the Noisy Quantum Gates documentation
======================================

**Quantum Gates** (/lu'make/) is a Python library for simulate the noisy 
behaviour of quantum devices. The noise is incorporated directly in the gates, 
which become stochastic matrices. 

How to install
--------------

Requirements
~~~~~~~~~~~~

The Python version should be 3.9 or later. We recommend using the library
together with a 
`IBM Quantum Lab <a href="https://quantum-computing.ibm.com/lab" target="_blank">`__ 
account, as it necessary for circuit compilation with Qiskit.

Installation as a user
~~~~~~~~~~~~~~~~~~~~~~

The library is available on the Python Package Index (PyPI) with
``pip install quantum-gates``.

Installation as a contributor
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For users who want to have access to the source code, we recommend cloning 
the repository from
`Github <a href="https://github.com/CERN-IT-INNOVATION/quantum-gates" target="_blank">`__.


.. note::

   This project is under active development.


Functionality
--------------

Gates
~~~~~

To sample quantum gates with the noise incorporated in them, one can set
up a :doc:`gates` instance. The methods of this object return the matrices
as numpy array. The sampling is stochastic, and one can set the numpy seed
to always get the same sequence of noise.


Factories
~~~~~~~~~

To produce :doc:`gates`, we use :doc:`factories`, such as the
:ref:`cnotfactory`. The instances of these classes have a construct()
method, with a well documented signature.

Pulses
~~~~~~

When constructing a set of quantum gates with the Gates class, one can
specify a :ref:`pulse`. This pulse describes the
shape of the RF pulses used to implement the gates.

Integrators
~~~~~~~~~~~

Behind the scenes, we solve Ito integrals to deal with the different
pulse shapes. This is handled by the :doc:`integrators`.

Simulate quantum circuits
-------------------------

Simulators
~~~~~~~~~~

The :doc:`simulators` can be used to simulate a quantum circuit transpiled 
with Qiskit with a specific noisy gate set.

Backends
~~~~~~~~

For the computation, we provide
:doc:`backends` out of the box, such as the :ref:`efficientbackend` that
uses optimized tensor contractions to simulate 20+ qubits with the
statevector method.

Circuits
~~~~~~~~

The simulators can be configured with a :doc:`circuits` class, such as 
:ref:`_efficient_circuit`. This class is responsible for sampling the 
noisy gates. The class can be configured with a :doc:`gates` instance and one of 
the :doc:`backends` that executes the statevector simulation. 

Legacy
------

We also provide the :doc:`legacy` implementations of the gates, simulator and
circuit classes. They can be used for unit testing.

Utility
-------

In performing quantum simulation, there are many steps that are
performed repeatedly, such as setup the IBM backend, transpiling the
quantum circuits, implementing well-known quantum circuits such as the
GHZ circuit, and executing the simulation in parallel on a powerful
machine. For this reason, the most frequently used functions are part of
the utilities.
