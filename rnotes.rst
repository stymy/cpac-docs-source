Release Notes
-------------

Version 0.3.4 Alpha - 2014.04.08
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
#. Added local Functional Connectivity Density (lFCD) measure to the Network Centrality options.

#. Added the ability to specify different centrality parameters for each of the measures (degree, eigenvector, lFCD).

#. Group-level analysis is now able to be run in parallel - simply set the amount of processors you wish to dedicate in the Group 

#. Analysis tab in the pipeline editor window under 'Number of Models to Run Simultaneously'.

#. The processing run timing feature is now more polished- look for a cpac_individual_timing_{pipeline name}.csv or cpac_group_timing_{pipeline name}.csv file in your output directory for a breakdown and comparison of information and run times from separate runs.

#. Introduced the option to turn on/off Z-score standardization of outputs - this can be found within the 'Derivatives Settings' tab in the pipeline editor.

#. GUI fixes and improvements, including errors involving naming the pipeline yaml file and the removal of redundant options.

#. Group level analysis models no longer overwrite each other within the working directory - all subcategories, ROIs, etc. retain their intermediary files for re-runs.

#. The 'Test Configuration' feature in the pipeline editor is now more robust.

#. ANTS anatomical registration no longer takes up more processors than has been assigned by the user.

#. Speed improvements for centrality functions, including new C-based code.

#. Setting the memory limit for centrality will now work appropriately. Number of voxels to compute connectivity maps for at once will be set to be equal to the memory limit.

#. Improved unit testing for dual regression, TSE and SCA

#. TSE can now handle masks and ROIs with floating point values

#. Pipeline config files with a leading number in their CPAC pipeline name will now load into the GUI properly


Instructions for Updating to 0.3.4
``````````````````````````````````
#. Download the new version from `Github <https://github.com/FCP-INDI/C-PAC>`_ or the `CPAC homepage <http://fcp-indi.github.io.>`_.

#. If you do not have Cython installed already, follow the instructions `here </install.html#install-python-dependencies>`.

#. Replace the old CPAC directory with the new files and then run ``sudo python setup.py install``.


Version 0.3.3 Alpha - 2013.12.31
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
#. CPAC is now compatible with Nipy's Nipype 0.9.

#. A major group-level analysis error was resolved.

#. Forking of strategies is now possible through the GUI (for example, running two different registration methods at the same time).

#. Significant useability improvements to the GUI.

#. You can now specify separate seeds for timeseries extraction only or timeseries extraction intended for seed correlation analysis (SCA).

#. A new "Test Configuration" option has been included in the pipeline editor in the GUI which enables users to test their setup before running the pipeline.

#. An issue where the network centrality workflow would use more cores than assigned has been resolved.

#. An issue where VMHC maps would only be generated in 2mm resolution despite what was assigned has been resolved.

#. An issue where the raw correlation map for SCA was only being generated for one seed has been resolved.

#. An issue where timeseries extraction and seed correlation analysis would not run for new seeds defined in the pipeline editor was resolved.


Version 0.3.2 Alpha - 2013.11.04
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
#. The option to use the `ANTS registration <http://stnava.github.io/ANTs/>`_ tool for anatomical registration has been introduced.

#. The option to toggle `Boundary Based Registration <http://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FLIRT_BBR>`_ on and off for functional to anatomical registration has been introduced.

#. Automatic QC page creation enabled.

#. Pipeline configuration files created by older versions of CPAC are now automatically checked for missing parameters.

#. There have been several assorted GUI fixes and improvements.


Version 0.3.1 Alpha - 2013.09.13
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
#. A range of improvements to the GUI and its operation.

#. Extended improvements to group analysis operation.

#. Error fix: custom FSL-FNIRT configuration files can now successfully be provided to CPAC.

#. Error fix: CPAC setup.py would not fully overwrite old files - setup.py now works correctly and also creates a backup folder with the old CPAC install directory.

#. Addition of some more informative and user-friendly error messages and user warnings.

#. CPAC pipeline configuration file renamed from config.yml to pipeline_config.yml.

#. Group analysis function update: the ability to classify EVs as either categorical or continuous has been temporarily removed as we continue our ongoing process of refining CPAC's group analysis model builder. The user must now provide a phenotypic file (.csv format) with categorical EVs broken out into dummy variables.

Version 0.1.9 Alpha - 2013.03.18
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
1) feature: Dual Regression for Spatial Maps and ROIs
2) feature/issue120: Flexibility with multiple models and model-specific subject list
3) feature/issue157: Condor cluster job submission support
4) fix/issue108: (re)check output directory when pipeline is run again
5) fix/issue147: Split up covariates if create_fsl_model.py when modeling group variances seperately
6) fix/issue139: Rename "sink" directory to "output" directory

Version 0.1.8 Alpha - 2013.2.20
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
1) Modification- replaced all configuration files(config.py, CPAC_subject_list.py, config_fsl.py, data_config.py) to YAML formats
2) Fix- Ignore empty lines and commented lines in all txt files used as input by CPAC
3) Fix - Configuration files import issue.  
4) Removed confusing directories with numbers for sca roi outputs and centrality outputs. Now all the ROI outputs go into a single directory per subject and same holds centrality outputs


Version 0.1.7 Alpha - 2013.02.05
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
1) Improved Error message for Removing Working Directory
2) New Centrality Workflow
3) Fixed underscore problem when no session in the data
4) FSL model file generator tool : one run, improved error reporting, multicollinearity detection
5) ROI , mask and template spefications are now files instead of directories
6) Anatomical and Functional Data can now be registered to different standard resolution templates
7) Subject processed fully notification after the subject pipeline finishes


Version 0.1.6 Alpha - 2013.01.21
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1) Fix logger in extract_data.py tool
2) Nuisance code Refactoring
3) Fixed ROI names in SCA
4) Added Import for create_fsl_model in local __init__.py
5) Added New Pipeline names
6) Fixed Pipeline Naming bug when package is installed
7) Centrality fix to handle NAN correlation values
8) Generate ROI nifti files using user co-ordinates
9) Fix output directory structure to handle multiple model run with single subject list
10) Fix in Group Analysis, to get 4D EPI as per input subject list
11) Boundary Based Registration becomes the default registration
12) New Alff/fAlff workflow
13) Updates in config file to accomodate new features
14) Fix to append unit of time(in TR) in slice timing correction: get_scan_parameters
15) Minor changes in create_fsl_model : replace '#' in output csv name with '__'
16) Feature addition to clear subject level working directory
17) Added Exception to handle missing dependancy for pygraphviz
18) Added extract_parameters.py script to consolidate motion parameters


Version 0.1.1 Alpha - 2012.10.15
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* **Scrubbing:** Users can now specify the number of TRs that should be removed before and after an offending TR.

* **Scrubbing:** C-PAC now prints a warning specifying the number of time points left after scrubbing. If no time points are left, C-PAC will crash and print an error.

* **Slice Timing:** Users can now specify which sites are run with slice timing correction.

* **Slice Timing:** Slice timing correction is now able to read slice timing information directly from an image file, and works on Multiband sequences.

* **Timeseries:** Users can now specify a different number of initial TRs to be removed for each site.

* **Data Config:** Data extraction now works for the NKI-TRT data set, and automatically extracts scan parameters for each subject from the image file.

* **Fix:** C-PAC no longer crashes if dot is not installed. Instead, it prints an error and contines running.



