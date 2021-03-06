Outputs and Measures
--------------------
Connectivity Measures
^^^^^^^^^^^^^^^^^^^^^
C-PAC provides users a full suite of connectivity measures, including:

* :doc:`Seed-based Correlation Analysis (SCA) </sca>` - Analyze the connectivity between brain regions.
* :doc:`Dual Regression </dual_reg>` - Compare large-scale networks.
* :doc:`Amplitude of Low Frequency Fluctuations (ALFF) and fractional ALFF (fALFF) </alff>` - Measure the power of slow fluctuations in brain activity.
* :doc:`Voxel-mirrored Homotopic Connectivity (VMHC) </vmhc>` - Investigate connectivity between hemispheres.
* :doc:`Boostrap Analysis of Stable Clusters (BASC) </basc>` - Quantify the stable characteristics of networks.
* :doc:`Regional Homogeneity (ReHo) </reho>` - Measure the similarity of activity patterns across neighboring voxels.
* :doc:`Network centrality </centrality>` - Analyze the structure of functional networks.
* :doc:`Connectome-wide Association Studies (CWAS) </cwas>` - Explore the examines the relationship between patterns of functional connectivity and phenotypes.

Timeseries Extraction
^^^^^^^^^^^^^^^^^^^^^
C-PAC makes it easy to :doc:`export timeseries information </tse>` from your data. Users can choose to extract timeseries from regions of interest, individual voxels, and even surface vertices (requires `FreeSurfer <http://surfer.nmr.mgh.harvard.edu/>`_).

FSL Group Analysis
^^^^^^^^^^^^^^^^^^
C-PAC utilizes the powerful statistical tools in `FSL <http://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FEAT>`_ to :doc:`compare findings across groups </fsl_ga>`.

.. toctree::
   :hidden: 

   Seed-based Correlation Analysis <sca>
   ALFF and fALFF <alff>
   Voxel-mirrored Homotopic Connectivity <vmhc>
   Boostrap Analysis of Stable Clusters <basc>
   Regional Homogeneity <reho>
   Network Centrality <centrality>
   Connectome-wide Association Studies <cwas>
   Timeseries Extraction <tse>
   Group Statistics <fsl_ga>