Module ants.core.ants_metric_io
===============================

Functions
---------

    
`create_ants_metric(fixed, moving, metric_type='MeanSquares', fixed_mask=None, moving_mask=None, sampling_strategy='regular', sampling_percentage=1)`
:   Arguments
    ---------
    metric_type : string
        which metric to use
        options:
            MeanSquares
            MattesMutualInformation
            ANTSNeighborhoodCorrelation
            Correlation
            Demons
            JointHistogramMutualInformation
    
    Example
    -------
    >>> import ants
    >>> fixed = ants.image_read(ants.get_ants_data('r16'))
    >>> moving = ants.image_read(ants.get_ants_data('r64'))
    >>> metric_type = 'Correlation'
    >>> metric = ants.create_ants_metric(fixed, moving, metric_type)

    
`new_ants_metric(dimension=3, precision='float', metric_type='MeanSquares')`
:   

    
`supported_metrics()`
: