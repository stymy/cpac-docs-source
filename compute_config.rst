Computer Settings
-----------------
.. figure:: /_images/gui/compute_gui.png

#. **Run CPAC on a Cluster/Grid:** Select False if you intend to run CPAC on a single machine. If set to True, CPAC will attempt to submit jobs through the job scheduler / resource manager selected below.

#. **FSL Path:** Full path to the FSL version to be used by CPAC. If you have specified an FSL path in your .bashrc file, this path will be set automatically.

#. **Job Scheduler / Resource Manager:** Sun Grid Engine (SGE) or Portable Batch System (PBS). Only applies if you are running on a grid or compute cluster.

#. **SGE Parallel Environment:** SGE Parallel Environment to use when running CPAC. Only applies when you are running on a grid or compute cluster using SGE.

#. **SGE Queue:** SGE Queue to use when running CPAC. Only applies when you are running on a grid or compute cluster using SGE.

#. **Number of Cores Per Subject:** Number of cores (on a single machine) or slots on a node (cluster/grid) per subject. Slots are cores on a cluster/grid node. Number of Cores Per Subject multiplied by Number of Subjects to Run Simultaneously must not be greater than the total number of cores.

#. **Number of Subjects to Run Simultaneously:** This number depends on computing resources.