# Troubleshooting

This page will cover common error messages, what they mean, and how to resolve them.

## FileExistsError

``` { .yaml .no-copy }
FileExistsError: [WinError 183] Cannot create a file when that file already exists:
'C:\\...\\xCropProtection\\run\\Rummen-xCP-TestingScenario'
```

**Explanation**:

A folder with the same name as `SimID` exists in the *\xCropProtection\run\\* folder.

**Possible solutions**:

- Delete or move the folder to run xCropProtection using that `SimID`.
- Change the `SimID` value to one that does not already exist in the *\xCropProtection\run\\* folder.

## ValueError: chunk shape

``` { .yaml .no-copy }
ValueError: Chunk shape must not be greater than data shape in any dimension. (1,) is not compatible with (0,)
```

**Explanation**:

The number of applied areas calculated by xCropProtection is different than the expected value. Incorrect or overly restrictive constraints on dates, fields, or crop type may result in zero applications being performed during the simulation.

**Possible solutions**:

- Check the value of `SimulationStart` and `SimulationEnd` in *template.xrun*. Compare these values to the `TemporalValidity` defined in all PPMCalendars used in the xCropProtection run. The `TemporalValidity` should overlap with the simulation start and end values.
- In all PPMCalendars, check `Application` elements' `ApplicationWindow` date ranges. It is possible that application windows are defined for days/months outside the simulation start and end values set in *template.xrun*.
- In all PPMCalendars, check the value of `TargetCrops`. Verify that this is an integer value and that one or more fields in the scenario have this crop type. In *\xCropProtection\scenario\\[scenario name]\geo\package.xinfo*, verify that `feature_type_attribute` refers to the correct field name. In the same file, verify that `base_landscape_geometries` refers to the correct shapefile.
- In all PPMCalendars, check the value of `TargetFields`. Verify that this is an integer value or list of integers and that one or more fields in the scenario have this ID. In *\xCropProtection\scenario\\[scenario name]\geo\package.xinfo*, verify that `feature_id_attribute` refers to the correct field name. In the same file, verify that `base_landscape_geometries` refers to the correct shapefile.

## ValueError: probability sum

``` { .yaml .no-copy }
ValueError: Probability sum is not 1.0!
```

**Explanation**:

The sum of probability values in one of the choice distributions defined in a PPMCalendar does not equal 1.0.

**Possible solutions**:

- Check the probability values in all PPMCalendars to ensure they sum to 1.0.
- xCropProtection allows a small amount of error when calculating the sum of a choice distribution's probability values. The sum is rounded to 5 decimal places to prevent floating-point arithmetic errors that may occur when adding floating-point values in python. Further explanation can be found on the [Python.org website](https://docs.python.org/3/tutorial/floatingpoint.html).