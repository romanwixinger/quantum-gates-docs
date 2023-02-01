Welcome to Quantum Gates documentation
======================================

**Lumache** (/lu'make/) is a Python library for cooks and food lovers
that creates recipes mixing random ingredients.
It pulls data from the `Open Food Facts database <https://world.openfoodfacts.org/>`_
and offers a *simple* and *intuitive* API.

Check out the :doc:`usage` section for further information, including
how to :ref:`installation` the project.


Gates
~~~~~

To sample quantum gates with the noise incorporated in them, one can set
up a :doc:`gates` instance. The methods of this object return the matrices
as numpy array. The sampling is stochastic, and one can set the numpy seed
to always get the same sequence of noise.


Factories
~~~~~~~~~

To produce gates, we use gate factories, such as the
:ref:`cnotfactory`. The instances of these classes have a construct()
method, with a well documented signature.

Pulses
~~~~~~

When constructing a set of quantum gates with the Gates class, one can
specify a `Pulse <./explanations/pulses.md>`__. This pulse describes the
shape of the RF pulses used to implement the gates.

Integrators
~~~~~~~~~~~

Behind the scenes, we solve Ito integrals to deal with the different
pulse shapes. This is handled by the
`Integrator <./explanations/integrators.md>`__ class.

Simulate quantum circuits
-------------------------

Simulators
~~~~~~~~~~

The `MrAndersonSimulator <./explanations/simulators.md>`__ can be used
to simulate a quantum circuit transpiled with Qiskit with a specific
noisy gate set.

Backends
~~~~~~~~

For the computation, we provide
`backends <./explanations/backends.md>`__ out of the box, such as the
`EfficientBackend <./explanations/backends.md#efficientbackend>`__ that
uses optimized tensor contractions to simulate 20+ qubits with the
statevector method.

Circuits
~~~~~~~~

The simulators can be configured with a
`circuit <./explanations/circuits.md>`__ class, such as
`EfficientCircuit <./explanations/circuits.md#efficientcircuit>`__. This
class is responsible for sampling the noisy gates. The class can be
configured with a specific `gateset <./explanations/gates.md>`__ and a
`backend <./explanations/backends.md>`__ that executes the statevector
simulation.

Legacy
------

We also provide the legacy implementations of the gates, simulator and
circuit classes. They can be used for unit testing.

Utility
-------

In performing quantum simulation, there are many steps that are
performed repeatedly, such as setup the IBM backend, transpiling the
quantum circuits, implementing well-known quantum circuits such as the
GHZ circuit, and executing the simulation in parallel on a powerful
machine. For this reason, the most frequently used functions are part of
the utilities.



.. note::

   This project is under active development.

Contents
--------

.. toctree::

   usage
   api
   overview
   gates
   factories
   pulses
   integrators
   simulators
   circuits
   backends
   circuit_generators
   utilities
   legacy

