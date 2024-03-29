Module ants.registration.interface
==================================
ANTsPy Registration

Functions
---------

    
`motion_correction(image, fixed=None, type_of_transform='BOLDRigid', mask=None, fdOffset=50, outprefix='', verbose=False, **kwargs)`
:   Correct time-series data for motion.
    
    ANTsR function: `antsrMotionCalculation`
    
    Arguments
    ---------
        image: antsImage, usually ND where D=4.
    
        fixed: Fixed image to register all timepoints to.  If not provided,
            mean image is used.
    
        type_of_transform : string
            A linear or non-linear registration type. Mutual information metric and rigid transformation by default.
            See ants registration for details.
    
        mask: mask for image (ND-1).  If not provided, estimated from data.
            2023-02-05: a performance change - previously, we estimated a mask
            when None is provided and would pass this to the registration.  this
            impairs performance if the mask estimate is bad.  in such a case, we
            prefer no mask at all.  As such, we no longer pass the mask to the
            registration when None is provided.
    
        fdOffset: offset value to use in framewise displacement calculation
    
        outprefix : string
            output will be named with this prefix plus a numeric extension.
    
        verbose: boolean
    
        kwargs: keyword args
            extra arguments - these extra arguments will control the details of registration that is performed. see ants registration for more.
    
    Returns
    -------
    dict containing follow key/value pairs:
        `motion_corrected`: Moving image warped to space of fixed image.
        `motion_parameters`: transforms for each image in the time series.
        `FD`: Framewise displacement generalized for arbitrary transformations.
    
    Notes
    -----
    Control extra arguments via kwargs. see ants.registration for details.
    
    Example
    -------
    >>> import ants
    >>> fi = ants.image_read(ants.get_ants_data('ch2'))
    >>> mytx = ants.motion_correction( fi )

    
`registration(fixed, moving, type_of_transform='SyN', initial_transform=None, outprefix='', mask=None, moving_mask=None, mask_all_stages=False, grad_step=0.2, flow_sigma=3, total_sigma=0, aff_metric='mattes', aff_sampling=32, aff_random_sampling_rate=0.2, syn_metric='mattes', syn_sampling=32, reg_iterations=(40, 20, 0), aff_iterations=(2100, 1200, 1200, 10), aff_shrink_factors=(6, 4, 2, 1), aff_smoothing_sigmas=(3, 2, 1, 0), write_composite_transform=False, random_seed=None, verbose=False, multivariate_extras=None, restrict_transformation=None, smoothing_in_mm=False, **kwargs)`
:   Register a pair of images either through the full or simplified
    interface to the ANTs registration method.
    
    ANTsR function: `antsRegistration`
    
    Arguments
    ---------
    fixed : ANTsImage
        fixed image to which we register the moving image.
    
    moving : ANTsImage
        moving image to be mapped to fixed space.
    
    type_of_transform : string
        A linear or non-linear registration type. Mutual information metric by default.
        See Notes below for more.
    
    initial_transform : list of strings (optional)
        transforms to prepend
    
    outprefix : string
        output will be named with this prefix.
    
    mask : ANTsImage (optional)
        Registration metric mask in the fixed image space.
    
    moving_mask : ANTsImage (optional)
        Registration metric mask in the moving image space.
    
    mask_all_stages : boolean
        If true, apply metric mask(s) to all registration stages, instead of just the final stage.
    
    grad_step : scalar
        gradient step size (not for all tx)
    
    flow_sigma : scalar
        smoothing for update field
        At each iteration, the similarity metric and gradient is calculated. 
        That gradient field is also called the update field and is smoothed 
        before composing with the total field (i.e., the estimate of the total 
        transform at that iteration). This total field can also be smoothed 
        after each iteration.
    
    total_sigma : scalar
        smoothing for total field
    
    aff_metric : string
        the metric for the affine part (GC, mattes, meansquares)
    
    aff_sampling : scalar
        number of bins for the mutual information metric
    
    aff_random_sampling_rate : scalar
        the fraction of points used to estimate the metric. this can impact
        speed but also reproducibility and/or accuracy.
    
    syn_metric : string
        the metric for the syn part (CC, mattes, meansquares, demons)
    
    syn_sampling : scalar
        the nbins or radius parameter for the syn metric
    
    reg_iterations : list/tuple of integers
        vector of iterations for syn. we will set the smoothing and multi-resolution parameters based on the length of this vector.
    
    aff_iterations : list/tuple of integers
        vector of iterations for low-dimensional (translation, rigid, affine) registration.
    
    aff_shrink_factors : list/tuple of integers
        vector of multi-resolution shrink factors for low-dimensional (translation, rigid, affine) registration.
    
    aff_smoothing_sigmas : list/tuple of integers
        vector of multi-resolution smoothing factors for low-dimensional (translation, rigid, affine) registration.
    
    random_seed : integer
        random seed to improve reproducibility. note that the number of ITK_GLOBAL_DEFAULT_NUMBER_OF_THREADS should be 1 if you want perfect reproducibility.
    
    write_composite_transform : boolean
        Boolean specifying whether or not the composite transform (and its inverse, if it exists) should be written to an hdf5 composite file. This is false by default so that only the transform for each stage is written to file.
    
    verbose : boolean
        request verbose output (useful for debugging)
    
    multivariate_extras : additional metrics for multi-metric registration
        list of additional images and metrics which will
        trigger the use of multiple metrics in the registration
        process in the deformable stage. Each multivariate metric needs 5
        entries: name of metric, fixed, moving, weight,
        samplingParam. the list of lists should be of the form ( (
        "nameOfMetric2", img, img, weight, metricParam ) ). Another
        example would be  ( ( "MeanSquares", f2, m2, 0.5, 0
          ), ( "CC", f2, m2, 0.5, 2 ) ) .  This is only compatible
        with the SyNOnly or antsRegistrationSyN* transformations.
    
    restrict_transformation : This option allows the user to restrict the
          optimization of the displacement field, translation, rigid or
          affine transform on a per-component basis. For example, if
          one wants to limit the deformation or rotation of 3-D volume
          to the first two dimensions, this is possible by specifying a
          weight vector of ‘(1,1,0)’ for a 3D deformation field or
          ‘(1,1,0,1,1,0)’ for a rigid transformation. Restriction
          currently only works if there are no preceding
          transformations.
    
    smoothing_in_mm : boolean ; currently only impacts low dimensional registration
    
    kwargs : keyword args
        extra arguments
    
    Returns
    -------
    dict containing follow key/value pairs:
        `warpedmovout`: Moving image warped to space of fixed image.
        `warpedfixout`: Fixed image warped to space of moving image.
        `fwdtransforms`: Transforms to move from moving to fixed image.
        `invtransforms`: Transforms to move from fixed to moving image.
    
    Notes
    -----
    type_of_transform can be one of:
        - "Translation": Translation transformation.
        - "Rigid": Rigid transformation: Only rotation and translation.
        - "Similarity": Similarity transformation: scaling, rotation and translation.
        - "QuickRigid": Rigid transformation: Only rotation and translation.
                        May be useful for quick visualization fixes.'
        - "DenseRigid": Rigid transformation: Only rotation and translation.
                        Employs dense sampling during metric estimation.'
        - "BOLDRigid": Rigid transformation: Parameters typical for BOLD to
                        BOLD intrasubject registration'.'
        - "Affine": Affine transformation: Rigid + scaling.
        - "AffineFast": Fast version of Affine.
        - "BOLDAffine": Affine transformation: Parameters typical for BOLD to
                        BOLD intrasubject registration'.'
        - "TRSAA": translation, rigid, similarity, affine (twice). please set
                    regIterations if using this option. this would be used in
                    cases where you want a really high quality affine mapping
                    (perhaps with mask).
        - "Elastic": Elastic deformation: Affine + deformable.
        - "ElasticSyN": Symmetric normalization: Affine + deformable
                        transformation, with mutual information as optimization
                        metric and elastic regularization.
        - "SyN": Symmetric normalization: Affine + deformable transformation,
                    with mutual information as optimization metric.
        - "SyNRA": Symmetric normalization: Rigid + Affine + deformable
                    transformation, with mutual information as optimization metric.
        - "SyNOnly": Symmetric normalization: no initial transformation,
                    with mutual information as optimization metric. Assumes
                    images are aligned by an inital transformation. Can be
                    useful if you want to run an unmasked affine followed by
                    masked deformable registration.
        - "SyNCC": SyN, but with cross-correlation as the metric.
        - "SyNabp": SyN optimized for abpBrainExtraction.
        - "SyNBold": SyN, but optimized for registrations between BOLD and T1 images.
        - "SyNBoldAff": SyN, but optimized for registrations between BOLD
                        and T1 images, with additional affine step.
        - "SyNAggro": SyN, but with more aggressive registration
                        (fine-scale matching and more deformation).
                        Takes more time than SyN.
        - "TV[n]": time-varying diffeomorphism with where 'n' indicates number of
            time points in velocity field discretization.  The initial transform
            should be computed, if needed, in a separate call to ants.registration.
        - "TVMSQ": time-varying diffeomorphism with mean square metric
        - "TVMSQC": time-varying diffeomorphism with mean square metric for very large deformation
        - "antsRegistrationSyN[x]": recreation of the antsRegistrationSyN.sh script in ANTs
                                    where 'x' is one of the transforms available (e.g., 't', 'b', 's')
        - "antsRegistrationSyNQuick[x]": recreation of the antsRegistrationSyNQuick.sh script in ANTs
                                    where 'x' is one of the transforms available (e.g., 't', 'b', 's')
        - "antsRegistrationSyNRepro[x]": reproducible registration.  x options as above.
        - "antsRegistrationSyNQuickRepro[x]": quick reproducible registration.  x options as above.
    
    Example
    -------
    >>> import ants
    >>> fi = ants.image_read(ants.get_ants_data('r16'))
    >>> mi = ants.image_read(ants.get_ants_data('r64'))
    >>> fi = ants.resample_image(fi, (60,60), 1, 0)
    >>> mi = ants.resample_image(mi, (60,60), 1, 0)
    >>> mytx = ants.registration(fixed=fi, moving=mi, type_of_transform = 'SyN' )