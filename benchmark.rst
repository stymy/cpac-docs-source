CPAC Benchmark Package
======================

The CPAC Benchmark Package consists of all of the data files, configuration files, and comparison scripts needed to test CPAC on your machine compare your outputs with a standard set of outputs processed by the CPAC team. Specifically, it contains:

* Anatomical and Functional images for 40 subjects (20 controls and 20 ADHD; a subset of the ADHD-200 dataset.)

* The configuration files (``benchmark_data_config.yml``, ``benchmark_config.yml``, and ``benchmark_fsl_config.yml``) needed to generate subject lists for these subjects and to run individual- and group-level analyses.

* Precomputed outputs for the same set of subjects, processed by the CPAC team.

* Python scripts to compare your outputs with ours.

The following instructions will guide you through the simple process of running the CPAC Benchmark test. This process should require about 30 minutes of your time (the actual data processing will take significantly longer, but requires no input from the user).

1) Install CPAC
^^^^^^^^^^^^^^^
Make sure you have also installed all of the dependencies and downloaded the required Image Resource Files.

2) Download the CPAC Benchmark Package
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
The CPAC Benchmark Package is split into two pieces:

* Raw data and configuration files needed to process said data (`click here to download <http://www.nitrc.org/frs/shownotes.php?release_id=2361>`_)
* Precomputed group analysis results from the same data set, group models, and comparison scripts (coming soon)

Once downloaded, these packages should be extracted (using the command ``tar -xzvf <filename>``) and their contents combined into a single directory with the following structure.

.. figure:: /_images/file_structure.png

3) Configure CPAC
^^^^^^^^^^^^^^^^^
Included in the CPAC Benchmark Package is a ``configure_cpac_benchmark.sh`` script that when run will automatically configure CPAC to run on your system. More specifically, it will edit the included configuration files to match the location of the CPAC Benchmark Package on your computer.

To run this script, navigate in terminal to the ``/scripts`` directory of the CPAC Benchmark Package and enter the command ``bash configure_cpac_benchmark.sh``. You will be asked to enter the path to the main CPAC Benchmark Package folder.

.. figure:: /_images/config_script.png

4) Generate Subject Lists
^^^^^^^^^^^^^^^^^^^^^^^^^
Open the CPAC GUI and click to create a new Subject List. In the Subject List Configuration window, select Load and navigate to the ``/configs`` directory of the CPAC Benchmark Package. Select ``benchmark_data_config.yml`` and hit OK. This will load load the pre-configured settings.

.. figure:: /_images/benchmark_data_config.png

Click Generate Subject Lists. You will be asked to specify a name for a configuratino file containing the newly entered settings, as well as for the subject list itself. 

4) Configure CPAC
^^^^^^^^^^^^^^^^^
In the main CPAC window, under Pipelines, click Load and select the ``benchmark_config.yml`` file located in the ``/configs`` directory of the CPAC Benchmark Package. A new pipeline will show up in the list window; select this pipeline and click Edit. This will load the Pipeline Configuration window.

.. figure:: /_images/benchmark_pipeline_config.png

The majority of the preprocessing and analysis settings will be preloaded, but there are a few system-specific options that must be edited by the user before running CPAC. 


5) Run Individual- and Group-Level Analyses
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Once you have configured CPAC, first run the Individual-Level analysis pipeline by clicking the appropriate button at the bottom of the main CPAC window. This will bring up a log window that displays the progress of the CPAC run. When the pipeline has finished, you will see a ``Workflow Complete`` message.

At this point, you can run the Group-Level analysis workflow, again by clicking the appropriate button in the main CPAC window; which will display the same kind of log window seen for the Individual-Level pipeline.


6) Compare Outputs
^^^^^^^^^^^^^^^^^^
Navigate to the ``/scripts`` directory of the CPAC Benchmark Package. Here you will find a number of scripts to facillitate comparison between the outputs you just generated and the reference outputs included in the Benchmark Package.

Though it is possible to compare individual outputs, we recommend beginning your comparison by examining the spatial correlation between the statistical maps output during group analysis. These can be found in the following locations:

* Reference Data: ``/path/to/cpac_benchmark/reference/outputs/pipeline_benchmark/group_analysis_results``

* User Data ``/path/to/cpac_benchmark/outputs/pipeline_benchmark/group_analysis_results``

We have created a bash script that will automatically compare outputs. 



Using the ``spatial_correlation.py`` script located in the scripts directory, you can compute the Pearson's r and Kendalls w correlation between a newly generated file and the same file from the reference outputs.

To run this script, simply type ``python spatial_correlation.py file1 file2``, replacing ``file1`` and ``file2`` with the files which you would like to compare.

It is also possible to view a scatterplot of voxelwise correlations of the values in two files. To do this, run the ``voxelwise_correlation.py`` script in the same manner as the script above.

Alternately, you may run the comparison scripts manually by following the instructions below:



