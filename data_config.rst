Subject List Setup
------------------
In order to run CPAC, you must specify a list of subjects and data files to process. This is done by generating a subject list file that contains information about each subject to be run, their associated image files, and (optionally) scan parameter information for use during :doc:`Slice Timing Correction </slice>`.

.. figure:: /_images/gui/data_config_gui.png



Defining File Path Templates
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
CPAC has been designed to process large, complex data sets, and supports processing of multiple scans per subject, multiple scan sessions, and multiple data acquisition sites with differing scan acquisition parameters. Because the file directory structures resulting from such data sets can be compex, it is necessary to manually define the location of the image files to be processed for each subject.

File path templates are defined by adding wildcard characters (``%s``) to the file path of each type of image file to be processed (anatomical and functional). For each file path, you will need to add two of these wildcard characters, one in the place of the acquistion site directory, and one in the place of the subject directory. For example, if the full paths to the image files for :file:`subject_01` were:: 

  /home/data/site_1/subject_1/anat/mprage.nii.gz
  /home/data/site_1/subject_1/func/rest.nii.gz

Then the file path templates would would be::

 anatomicalTemplate = '/home/data/%s/%s/anat/mprage.nii.gz'
 functionalTemplate = '/home/data/%s/%s/func/rest.nii.gz'

It should be noted that C-PAC currently requires subject directories to be within a site level directory. If your data set does not contain scans from multiple acquisition sites, we recommend creating a dummy :file:`site_1` directory and placing subject files inside this directory. This peculiarity will be fixed in future versions of C-PAC.

In cases where file paths differ in more than just the site and subject directories, asterisks can be used. This is useful for data sets containing multiple scans per subject, multiple scan sessions, or subject-specific information in file or folder names. You may use as many asterisks as necessary to to define your file path templates. For example, if the paths to functional image files for a subject were::

    /home/data/site_1/subject_1/s01_func/session_1/rest_1.nii.gz
    /home/data/site_1/subject_1/s01_func/session_1/rest_2.nii.gz
    /home/data/site_1/subject_1/s01_func/session_2/rest_1.nii.gz
    /home/data/site_1/subject_1/s01_func/session_2/rest_2.nii.gz

The file path template would be::

    functionalTemplate = '/home/data/%s/%s/*_func/session_*/rest_*.nii.gz'

Example File Path Templates
"""""""""""""""""""""""""""
The image below illustrates the file structure used by the `1000 Functional Connectomes <http://fcon_1000.projects.nitrc.org/fcpClassic/FcpTable.html>`_ data release and the resulting file path templates.

.. figure:: /_images/fcon_structure.png

Another example is the file structure used by the `ABIDE <http://fcon_1000.projects.nitrc.org/indi/abide/>`_ and `ADHD-200 <http://fcon_1000.projects.nitrc.org/indi/adhd200/>`_ releases.

.. figure:: /_images/abide_adhd_structure.png

A final example is the file structure used by the `Enhanced Nathan Kline Institute-Rockland Sample <http://fcon_1000.projects.nitrc.org/indi/enhanced/>`_.

.. figure:: /_images/nki-rs_template.png

Users experiencing difficulties defining file path templates may want to re-organize their data to match one of the examples above. If you manually define a file path template and encounter an error when attempting to generate subject lists, please :doc:`contact us </help>` and we will be happy to help.

Additionally, if you are using one of the datasets released by INDI (1000 Functional Connectomes, ADHD-200, ABIDE, NKI-RS, etc.), we provide 

Selectively Include or Exclude Subjects
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
By default, C-PAC will process data for all subjects matching the file templates defined above. In many cases however, a user may want to run only a subset of the subjects within a particular data set. In others, a user may want to exclude particular subjects from analysis. This can be done by specifying a list of subjects through the :file:`subjectList` or :file:`exclusionSubjectList` options. Lists can be specified either as a text file or directly in :file:`data_config.yml`. Text files should contain one subject ID per line, with each subject ID matching the name of a subject folder. The same steps can used with the :file:`siteList` option to selectively process data from specific acquisition sites.

Set Up Slice Timing Correction
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
If you wish to run :doc:`Slice Timing Correction </slice>`, you must specify the path to a spreadsheet file containing scan acquisition parameters and slice timing information. Instructions for creating this file can be :doc:`found here </slice>`, and we provide preconfigured versions for INDI data releases on the :doc:`Preconfigured Files </files>` page. If you do not wish to run Slice Timing Correction, set :file:`scanParametersCSV = None`.

Generate Subject Lists
^^^^^^^^^^^^^^^^^^^^^^
When you are done setting up :file:`data_config.yml`, save your changes. If you are using a :doc:`preconfigured file </files>`, make sure that the file templates have been modified to match the specific location of files on your system.

In the terminal, navigate to the directory where you would like to store subject lists for use by C-PAC. Open iPython by typing :file:`ipython`. From the iPython prompt, run one of the following commands.

If you are not running Slice Timing Correction, or all subjects within a site have the same acquisition order::

  import CPAC
  CPAC.utils.extract_data.run ('/path/to/data_config.yml')

If you are running Slice Timing Correction and subjects within a site have differing acquisition orders::

  import CPAC
  CPAC.utils.extract_data_multiscan_params.run ('/path/to/data_config.yml')

This will ouput three files needed to run C-PAC:

* :file:`CPAC_subject_list.yml` - Subject list used when running preprocessing and individual-level analyses. Contains subject IDs and paths to their associated data files.
* :file:`template_phenotypic.csv` - Used by the :doc:`FSL Model Script </fsl_ga>`.
* :file:`subject_list_group_analysis.txt` - Subject list used when running group-level analyses.

