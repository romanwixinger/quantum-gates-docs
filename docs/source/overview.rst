Overview
========

In this document you get an overview of the different classes and
functions. We focus on describing the purpose of the objects and refer
to the `explanation folder <./explanations/>`__ for the details.

Constructing noisy quantum gates
--------------------------------

Gates
~~~~~

To sample quantum gates with the noise incorporated in them, one can set
up a `Gates <./explanations/gates.md>`__ instance. The methods of this
object return the matrices as numpy array. The sampling is stochastic,
and one can set the numpy seed to always get the same sequence of noise.

Factories
~~~~~~~~~

To produce gates, we use gate factories, such as the
`CNOTFactory <./explanations/factories.md#cnotfactory>`__. The instances
of these classes have a construct() method, with a well documented
signature.

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
