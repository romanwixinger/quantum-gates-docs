Noisy Quantum Gates |Made at CERN!| |Made at CERN!| |Made at CERN!|
===================================================================

Implementation of the Noisy Quantum Gates model, which is soon to be
published. It is a novel method to simulate the noisy behaviour of
quantum devices by incorporating the noise directly in the gates, which
become stochastic matrices.

How to install
--------------

Requirements
~~~~~~~~~~~~

The Python version should be 3.9 or later. Find your Python version by
typing ``python`` or ``python3`` in the CLI. We recommend using the repo
together with a `IBM Quantum
Lab <https://quantum-computing.ibm.com/lab>`__ account, as it necessary
for circuit compilation with Qiskit in many cases.

Installation as a user
~~~~~~~~~~~~~~~~~~~~~~

The library is available on the Python Package Index (PyPI) with
``pip install quantum-gates``.

Installation as a contributor
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For users who want to have control over the source code, we recommend
the following installation. Clone the repository from
`Github <https://github.com/CERN-IT-INNOVATION/quantum-gates>`__, create
a new virtual environment, and activate the environment. Then you can
build the wheel and install it with the package manager of your choice
as described in the section `How to contribute <#how-to-contribute>`__.
This will install all dependencies in your virtual environment, and
install a working version of the library.

Quickstart
----------

Just run `simulation_demo.py <./docs/tutorials/simulation_demo.py>`__ or
execute the following code in a notebook. Make sure that the working
directory is the repository itself. Moreover, add your token to
configuration/token.py by defining it as the variable IBM_TOKEN =
“your_token”.

.. code:: python

   # Standard libraries
   import numpy as np
   import json

   # Qiskit
   from qiskit import QuantumCircuit, transpile
   from qiskit.visualization import plot_histogram

   # Own library
   from quantum_gates.simulators import MrAndersonSimulator
   from quantum_gates.gates import standard_gates
   from quantum_gates.circuits import EfficientCircuit
   from quantum_gates.utilities import DeviceParameters
   from quantum_gates.utilities import setup_backend
   IBM_TOKEN = "<your_token>"

We create a quantum circuit with Qiskit.

.. code:: python

   circ = QuantumCircuit(2,2)
   circ.h(0)
   circ.cx(0,1)
   circ.barrier(range(2))
   circ.measure(range(2),range(2))
   circ.draw('mpl')

Load the configurations from a `json
file <./docs/tutorials/simulation_demo_configuration.json>`__\ …

.. code:: python

   with open("docs/tutorial/simulation_demo_configuration.json", "r") as f:
       config = json.load(f)

… and setup the Qiskit backend later used for circuit transpilation.

.. code:: python

   backend_config = config["backend"]
   backend = setup_backend(Token=IBM_TOKEN, **backend_config)
   run_config = config["run"]

This allows us to load the `device
parameters <./docs/explanations/utilities.md#deviceparameters>`__, which
represent the noise of the quantum hardware.

.. code:: python

   qubits_layout = run_config["qubits_layout"]
   device_param = DeviceParameters(qubits_layout)
   device_param.load_from_backend(backend)
   device_param_lookup = device_param.__dict__()

Last, we perform the simulation …

.. code:: python

   sim = MrAndersonSimulator(gates=standard_gates, CircuitClass=EfficientCircuit)

   t_circ = transpile(
       circ,
       backend,
       scheduling_method='asap',
       initial_layout=qubits_layout,
       seed_transpiler=42
   )

   probs = sim.run(
       t_qiskit_circ=t_circ, 
       qubits_layout=qubits_layout, 
       psi0=np.array(run_config["psi0"]), 
       shots=run_config["shots"], 
       device_param=device_param_lookup,
       nqubit=2)

   counts_ng = {format(i, 'b').zfill(2): probs[i] for i in range(0, 4)}

… and analyse the result.

.. code:: python

   plot_histogram(counts_ng, bar_labels=False, legend=['Noisy Gates simulation'])

Usage
=====

We recommend to read the `overview <./docs/overview.md>`__ of the
documentation as a 2-minute preparation.

Imports
-------

There are two ways of importing the package. 1) If you installed the
code with pip, then the imports are simply of the form seen in the
`Quickstart <#quickstart>`__.

.. code:: python

   from quantum_gates.simulators import MrAndersonSimulator
   from quantum_gates.gates import standard_gates
   from quantum_gates.circuits import EfficientCircuit
   from quantum_gates.utilities import DeviceParameters, setup_backend

2) If you use the source code directly and develop within the
   repository, then the imports become

.. code:: python

   from src.quantum_gates._simulation.simulator import MrAndersonSimulator
   from src.quantum_gates._gates.gates import standard_gates
   from src.quantum_gates._simulation.circuit import EfficientCircuit
   from src.quantum_gates._utility.device_parameters import (
       DeviceParameters, 
       setup_backend
   )

Functionality
=============

The main components are the `gates <./docs/explanations/gates.md>`__,
and the `simulator <./docs/explanations/simulators.md>`__. One can
configure the gates with different `pulse
shapes <./docs/explanations/pulses.md>`__, and the simulator with
different `circuit classes <./docs/explanations/circuits.md>`__ and
`backends <./docs/explanations/backends.md>`__. The circuit classes use
a specific backend for the statevector simulation. The
`EfficientBackend <./docs/explanations/backends.md#efficientbackend>`__
has the same functionality as the
`StandardBackend <./docs/explanations/backends.md#standardbackend>`__,
but is much more performant thanks to optimized tensor contraction
algorithms. We also provide
`generators <./docs/explanations/circuit_generators.md>`__ for various
circuits, and scripts to run the circuits with the simulator, the IBM
simulator, and a real IBM backend. Last, all functionality is unit
tested and one can get sample code from the `unit tests <./tests/>`__.

How to contribute
=================

Contributions are welcomed and should apply the usual git-flow: fork
this repo, create a local branch named ‘feature-…’. Commit often to
ensure that each commit is easy to understand. Name your commits
‘[feature-…] Commit message.’, such that it possible to differentiate
the commits of different features in the main line. Request a merge to
the mainline often. Please remember to follow the `PEP 8 style
guide <https://peps.python.org/pep-0008/>`__, and add comments whenever
it helps. The corresponding `authors <#authors>`__ are happy to support
you.

Build
-----

You may also want to create your own distribution and test it. Navigate
to the repository in your CLI of choice. Build the wheel with the
command ``python3 -m build --sdist --wheel .`` and navigate to the
distribution with ``cd dist``. Use ``ls`` to display the name of the
wheel, and run ``pip install <filename>.whl`` with the correct filename.
Now you can use your version of the library.

Authors
=======

This project has been developed thanks to the effort of the following
people:

-  Giovanni Di Bartolomeo
-  Michele Vischi
-  Francesco Cesa
-  Michele Grossi (michele.grossi@cern.ch)
-  Sandro Donadi
-  Angelo Bassi
-  Roman Wixinger (roman.wixinger@gmail.com)

.. |Made at CERN!| image:: https://img.shields.io/badge/CERN-CERN%20openlab-brightgreen
   :target: https://openlab.cern/
.. |Made at CERN!| image:: https://img.shields.io/badge/CERN-Open%20Source-%232980b9.svg
   :target: https://home.cern
.. |Made at CERN!| image:: https://img.shields.io/badge/CERN-QTI-blue
   :target: https://quantum.cern/our-governance
