Module ants.registration.landmark_transforms
============================================

Functions
---------

    
`fit_time_varying_transform_to_point_sets(point_sets, time_points=None, initial_velocity_field=None, number_of_time_steps=None, domain_image=None, number_of_fitting_levels=4, mesh_size=1, spline_order=3, displacement_weights=None, number_of_compositions=10, composition_step_size=0.5, number_of_integration_steps=100, sigma=0.0, convergence_threshold=1e-06, rasterize_points=False, verbose=False)`
:   Estimate a time-varying transform from corresponding point sets (> 2).
    
    ANTsR function: fitTimeVaryingTransformToPointSets
    
    Arguments
    ---------
    point_sets : list of arrays
        Corresponding points across sets specified in physical space as a n x d matrix where n
        is the number of points and d is the dimensionality.
    
    time_points : array of ordered scalars between 0 and 1
        Set of scalar values, one for each point-set, designating its time position in the velocity
        flow.  If not set, it defaults to equal spacing between 0 and 1.
    
    initial_velocity_field : initial ANTs velocity field
        Optional velocity field for initializing optimization.  Overrides the number of integration
        points.
    
    number_of_time_steps : integer
        Time-varying velocity field parameter.  Needs to be equal to or greater than the number of
        point sets.  If not specified, it defaults to the number of point sets.
    
    domain_image : ANTs image
        Defines physical domain of the nonlinear transform.  Must be defined.
    
    number_of_fitting_levels : integer
        Integer specifying the number of fitting levels for the B-spline interpolation of the
        displacement field.
    
    mesh_size : integer or array
        Defines the mesh size at the initial fitting level for the B-spline interpolation of the
        displacement field..
    
    spline_order : integer
        Spline order of the B-spline displacement field.
    
    displacement_weights : array
        Defines the individual weighting of the corresponding scattered data value.  Default = NULL
        meaning all displacements are weighted the same.
    
    number_of_compositions : integer
        Total number of compositions.
    
    composition_step_size : scalar
        Scalar multiplication factor of the weighting of the update field.
    
    number_of_integration_steps : scalar
        Number of steps used for integrating the velocity field.
    
    sigma : scalar
        Gaussian smoothing standard deviation of the update field (in mm).
    
    convergence_threshold : scalar
        Composition-based convergence parameter using a window size of 10 values.
    
    rasterize_points : boolean
        Use nearest neighbor rasterization of points for estimating the update field (potential
        speed-up).  Default = False.
    
    verbose : bool
        Print progress to the screen.
    
    Returns
    -------
    
    ANTs transform
    
    Example
    -------
    >>> import ants
    >>> import numpy as np

    
`fit_transform_to_paired_points(moving_points, fixed_points, transform_type='affine', regularization=1e-06, domain_image=None, number_of_fitting_levels=4, mesh_size=1, spline_order=3, enforce_stationary_boundary=True, displacement_weights=None, number_of_compositions=10, composition_step_size=0.5, sigma=0.0, convergence_threshold=1e-06, number_of_time_steps=2, number_of_integration_steps=100, rasterize_points=False, verbose=False)`
:   Estimate a transform from corresponding fixed and moving landmarks.
    
    ANTsR function: fitTransformToPairedPoints
    
    Arguments
    ---------
    moving_points : array
        Moving points specified in physical space as a n x d matrix where n is the number
        of points and d is the dimensionality.
    
    fixed_points : array
        Fixed points specified in physical space as a n x d matrix where n is the number
        of points and d is the dimensionality.
    
    transform_type : character
        'rigid', 'similarity', "affine', 'bspline', 'tps', 'diffeo', 'syn', or 'time-varying (tv)'.
    
    regularization : scalar
        Ridge penalty in [0,1] for linear transforms.
    
    domain_image : ANTs image
        Defines physical domain of the nonlinear transform.  Must be defined for nonlinear
        transforms.
    
    number_of_fitting_levels : integer
        Integer specifying the number of fitting levels for the B-spline interpolation of the
        displacement field.
    
    mesh_size : integer or array
        Defines the mesh size at the initial fitting level for the B-spline interpolation of the
        displacement field.
    
    spline_order : integer
        Spline order of the B-spline displacement field.
    
    enforce_stationary_boundary : boolean
        Ensure no displacements on the image boundary (B-spline only).
    
    displacement_weights : array
        Defines the individual weighting of the corresponding scattered data value.  Default = NULL
        meaning all displacements are weighted the same.
    
    number_of_compositions : integer
        Total number of compositions for the diffeomorphic transforms.
    
    composition_step_size : scalar
        Scalar multiplication factor of the weighting of the update field for the diffeomorphic transforms.
    
    sigma : scalar
        Gaussian smoothing standard deviation of the update field (in mm).
    
    convergence_threshold : scalar
        Composition-based convergence parameter for the diff. transforms using a
        window size of 10 values.
    
    number_of_time_steps : integer
        Time-varying velocity field parameter.
    
    number_of_integration_steps : scalar
        Number of steps used for integrating the velocity field.
    
    rasterize_points : boolean
       Use nearest neighbor rasterization of points for estimating the update
       field (potential speed-up).  Default = False.
    
    verbose : bool
        Print progress to the screen.
    
    Returns
    -------
    
    ANTs transform
    
    Example
    -------
    >>> import ants
    >>> import numpy as np
    >>> fixed = np.array([[50.0,50.0],[200.0,50.0],[200.0,200.0]])
    >>> moving = np.array([[50.0,50.0],[50.0,200.0],[200.0,200.0]])
    >>> xfrm = ants.fit_transform_to_paired_points(moving, fixed, transform_type="affine")
    >>> xfrm = ants.fit_transform_to_paired_points(moving, fixed, transform_type="rigid")
    >>> xfrm = ants.fit_transform_to_paired_points(moving, fixed, transform_type="similarity")
    >>> domain_image = ants.image_read(ants.get_ants_data("r16"))
    >>> xfrm = ants.fit_transform_to_paired_points(moving, fixed, transform_type="bspline", domain_image=domain_image, number_of_fitting_levels=5)
    >>> xfrm = ants.fit_transform_to_paired_points(moving, fixed, transform_type="diffeo", domain_image=domain_image, number_of_fitting_levels=6)