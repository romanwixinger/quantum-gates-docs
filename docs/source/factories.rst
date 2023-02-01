Factories
=========

The gate factories stochasticall generate Noisy Quantum Gates as numpy
matrices.

Theory
------

The two main factors that influence the distribution of noisy gates are
the following. First, the `device
parameters <./utilities.md#deviceparameters>`__ for a specific quantum
device, containing information such as the T1, T2 times. Second, the
`pulse shape <./pulses.md>`__ used to execute a specific gate. While the
pulse shape is independent of the qubit we act on, the device parameters
are qubit specific. Thus, we choose to add the pulse shape as attribute
of the gate factory, while the specific noise parameters are provided as
method arguments when creating a gate.

Usage
-----

The are two types of classes, namely the ones representing pure noise
and the ones representing the noisy gates. The former do not need the
pulse as argument, as they do not come from the execution of a gate, and
thus the pulse does not matter.

.. code:: python

   from quantum_gates.factories import (
       BitflipFactory, 
       DepolarizingFactory,
       RelaxationFactory
   )

   bitflip_factory = BitflipFactory()

   tm = ...    # measurement time in ns
   rout = ...  # readout error 
   bitflip_gate = bitflip_factory.construct(tm, rout)

In the latter, we specify the pulse shape used in the execution of the
gates.

.. code:: python

   from quantum_gates.factories import (
       SingleQubitGateFactory,
       XFactory, 
       SXFactory, 
       CRFactory, 
       CNOTFactory,
       CNOTInvFactory
   )
   from quantum_gates.pulses import GaussianPulse

   pulse = GaussianPulse(loc=0.5, scale=0.5)
   x_factory = XFactory(pulse)

   phi = ...   # Phase of the drive defining axis of rotation on the Bloch sphere
   p = ...     # Single-qubit depolarizing error probability
   T1 = ...    # Qubit's amplitude damping time in ns 
   T2 = ...    # Qubit's dephasing time in ns
   x_gate = x_factory.construct(phi, p, T1, T2)

Classes
~~~~~~~

The interface of the classes can be found in the source code.

BitflipFactory
~~~~~~~~~~~~~~

See `here <../../src/quantum_gates/_gates/factories.py#L7>`__ for
interface.

DepolarizingFactory
~~~~~~~~~~~~~~~~~~~

See `here <../../src/quantum_gates/_gates/factories.py#L30>`__ for
interface.

RelaxationFactory
~~~~~~~~~~~~~~~~~

See `here <../../src/quantum_gates/_gates/factories.py#L58>`__ for
interface.

SingleQubitGateFactory
~~~~~~~~~~~~~~~~~~~~~~

See `here <../../src/quantum_gates/_gates/factories.py#L100>`__ for
interface.

XFactory
~~~~~~~~

See `here <../../src/quantum_gates/_gates/factories.py#L291>`__ for
interface.

SXFactory
~~~~~~~~~

See `here <../../src/quantum_gates/_gates/factories.py#L315>`__ for
interface.

CRFactory
~~~~~~~~~

See `here <../../src/quantum_gates/_gates/factories.py#L337>`__ for
interface.

CNOTFactory
~~~~~~~~~~~

See `here <../../src/quantum_gates/_gates/factories.py#L599>`__ for
interface.

CNOTInvFactory
~~~~~~~~~~~~~~

See `here <../../src/quantum_gates/_gates/factories.py#L648>`__ for
interface.
