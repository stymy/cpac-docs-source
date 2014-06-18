Seed-based Correlation Analysis (SCA)
-------------------------------------
Connectivity in the Brain
^^^^^^^^^^^^^^^^^^^^^^^^^
Brain connectivity can refer to multiple distinct concepts, and it is important to understand the differences between them. When referring to anatomy, connectivity may refer to physical connections between brain areas, such as the long-distance fiber tracts revealed through methods such as Diffusion Tensor Imaging. Another form of connectivity that is commonly discussed in the literature is "functional connectivity", which is what we will be focusing on here.

What is Functional Connectivity?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Perhaps the most confusing thing to understand about functional connectivity is that in most cases, connectivity is never actually measured. This is because the term "functional connectivity" has come to refer to similarities in patterns of brain activity between regions. Two regions are said to be functionally connected if the time series of their activity is highly correlated. The reasoning behind this definition is that brain areas with similar activity patterns are likely to be communicating and sharing information.

Seed-based Correlation Analysis
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Seed-based Correlation Analysis (SCA) is one of the most common ways to explore functional connectivity within the brain. Based on the time series of a seed voxel (or ROI), connectivity is calcualted as the correlation of time series for all other voxels in the brain. The result of SCA is a connectivity map showing Z-scores for each voxel indicating how well it's time series correlates with the time series of the seed. Below is an example connectivity map showing correlated voxels based on a seed in the precuneus.

.. figure:: /_images/sca_map.png

Astute readers will note that the pattern of connectivity mapped above closely resembles the anatomy of the Default Network. Indeed, SCA may be used to explore functional networks that share similar patterns of activity.

Configuring C-PAC
^^^^^^^^^^^^^^^^^
**Before SCA can be calcualted, one must first extract a seed time series from which to calculate correlation.** This is done by configuring and running :doc:`Time Series Extraction </tse>`.

As such, many of the steps required to configure SCA (such as specifying an ROI) are found under :doc:`Time Series Extraction </tse>`. The following setting in :file:`config.yml` is used to turn on/off SCA::

    # Run Seed-based Correlation Analysis
    runSCA = [0]

External Resources
^^^^^^^^^^^^^^^^^^
* `mindhive - ConnectivityFAQ <http://mindhive.mit.edu/node/58>`_
* `Brain Connectivity - Scholarpedia <http://www.scholarpedia.org/article/Brain_connectivity>`_

