Anatomical Preprocessing
------------------------

Anatomical Registration
^^^^^^^^^^^^^^^^^^^^^^^
In order to compare brain activations between subjects, individual functional and anatomical images must first be transformed to match a common template. The most commonly used template (`MNI152 <http://www.bic.mni.mcgill.ca/ServicesAtlases/ICBM152NLin2009>`_) is maintained by the Montreal Neurological Institute, and is created by combining data from the brains of many different individuals to create an "average" brain. The image below shows how an individual brain is warped to match the shape of the template.

.. figure:: /_images/registration.png

CPAC provides the option of either using FSL (`FLIRT <http://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FLIRT>`_ and `FNIRT <http://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FNIRT>`_) or `Advanced Normalization Tools (ANTS) <http://stnava.github.io/ANTs/>`_ to register images. Although the use of ANTS requires an extra step during the CPAC install process, we have found its results to significantly better than those produced by FSL (a conclusion supported by a `recent systematic analysis by Klein et al. <http://mindboggle.info/papers/evaluation_NeuroImage2010.php>`_ )

During registration, individual anatomical images are first transformed to match the common template. Then, the functional data for each subject is registered to their own transformed anatomical image. Finally, functional derivative files are transformed to the common template. For more detail on how CPAC computes these steps, please see the `Registration Page of the developer documentation <http://fcp-indi.github.io/docs/developer/workflows/registration.html>`_.

By default, CPAC will register subject brains to the MNI152 template included with FSL. Users wishing to register their data to a different template (such as a group specific template) can specifiy alternative template files.

Configuring CPAC to run Anatomical Registration
"""""""""""""""""""""""""""""""""""""""""""""""
.. figure:: /_images/gui/anat_reg_gui.png

#. **Run Anatomical Registration:** Register anatomical images to a template.

#. **Anatomical Template Resolution:** The resolution to which anatomical images should be transformed during registration. This is the resolution at which processed anatomical files will be output.

#. **Anatomical Template (Brain Only):** Template to be used during registration. It is not necessary to change this path unless you intend to use a non-standard template.

#. **Anatomical Template (With Skull:** Template to be used during registration. It is not necessary to change this path unless you intend to use a non-standard template.

#. **Registration Method:** Registration methods to be used. Options are `ANTS <http://stnava.github.io/ANTs/>`_ and `FSL <http://fsl.fmrib.ox.ac.uk/fslcourse/lectures/practicals/reg/>`_.

#. **FNIRT Configuration File:** Configuration file specifying settings used during regisration. Required if FSL is selected as the registration method. This file can be found in the :file:`/etc/flirtsch` directory of your FSL install.

Anatomical Tissue Segmentation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
CPAC uses `FSL/FAST <http://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FAST>`_ to automatically segment brain images into white matter, gray matter, and CSF. This is done using probability maps that contain information about the likelihood that a given voxel will be of a particular tissue type. Users specify a probability threshold such that voxels meeting a minimum probability of being a particular tissue will be classified as such. This results in masks containing voxels of only a single tissue type.

.. figure:: /_images/segmentation.png

The default tissue probability maps (referred to as Prior Probability Maps) used during segmentation are based on information from a large number of brains, and are based on the priors distributed with FSL and are included in the "Image Resource Files" package downloaded during installation. For more detail on how CPAC computes these steps, please see the `Segmentation Page of the developer documentation <http://fcp-indi.github.io/docs/developer/workflows/seg_preproc.html>`_.

If you would like to use different priors, they must first be binarized such that for each voxel the probability for each tissue type is set to either 0% or 100%.

The following bash script will binarize existing priors::

    # Define what kind of priors to generate (gray, white, or csf)
    tissue=gray

    # Define threshold to use when binarizing data
    threshold=0.5

    # Copy existing priors (in this example, from FSL)
    3dcopy $FSL_DIR/data/standard/tissuepriors/avg152T1_${tissue}.hdr avg152T1_${tissue}.nii.gz

    # Binarize image using threshold set above
    fslmaths avg152T1_${tissue}.nii.gz -thr $threshold -bin avg152T1_${tissue}_2mm_bin

Configuring CPAC to run Anatomical Tissue Segmentation
""""""""""""""""""""""""""""""""""""""""""""""""""""""
.. figure:: /_images/gui/seg_gui.png

#. **Run Tissue Segmentation:** Automatically segment anatomical images into white matter, gray matter, and CSF based on prior probability maps.

#. **White Matter Probability Threshold:** Only voxels with a White Matter probability greater than this value will be classified as White Matter. Can be a single value or a list of values separated by commas.

#. **Gray Matter Probability Threshold:** Only voxels with a Gray Matter probability greater than this value will be classified as Gray Matter. Can be a single value or a list of values separated by commas.

#. **CSF Probability Threshold:** Only voxels with a CSF probability greater than this value will be classified as CSF. Can be a single value or a list of values separated by commas.

#. **Priors Directory:** Full path to a directory containing binarized prior probability maps. These maps are included as part of the 'Image Resource Files' package available on the Install page of the User Guide. It is not necessary to change this path unless you intend to use non-standard priors.

#. **White Matter Prior Probability Map:** Full path to a binarized White Matter prior probability map. It is not necessary to change this path unless you intend to use non-standard priors.

#. **Gray Matter Prior Probability Map:** Full path to a binarized Gray Matter prior probability map. It is not necessary to change this path unless you intend to use non-standard priors.

#. **CSF Prior Probability Map:** Full path to a binarized CSF prior probability map. It is not necessary to change this path unless you intend to use non-standard priors.


