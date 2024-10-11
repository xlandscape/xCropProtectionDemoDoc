# xToxicLoad parameterization

This page describes all files needed to parameterize and run xToxicLoad.

## template.xrun

In xToxicLoad, the user parameterization file is located in the root folder (*xToxicLoad*) with the .xrun file extension. This file can be written in XML or YAML.

### YAML

YAML is a human-friendly data serialization language that works well for configuration files. A sample YAML configuration file is shown below:

``` yaml title="template.xrun"
# $schema: ./model/variant/parameters.json
Project: scenario/Rummen-xToxicLoad-Test
SimID: xToxicLoad-Test
SimulationStart: 2020-01-01
SimulationEnd: 2022-12-31
CropProtectionScenario: test-xToxicLoad
SubstanceAndProductProperties: Substance and product properties - test1
NumberMC: 1
ParallelProcesses: 1
```

The schema for this file is located in the *xToxicLoad/model/variant* folder and describes the constraints for each key/value pair (in this file a key/value pair is two strings of text separated by a colon).

### XML

Here, the XML language is used to construct and transmit data to the xToxicLoad component. A sample XML configuration file is shown below (all comments removed):

``` xml title="template.xrun"
<?xml version="1.0" encoding="utf-8"?>
<Parameters>
  <Modeller>abc</Modeller>
  <Project>scenario/Rummen-xToxicLoad-Test</Project>
  <CropProtectionScenario>xCropProtection-Rummen</CropProtectionScenario>
  <ProductDatabase>CropProtection/product-database.db</ProductDatabase>
  <SimulationStart>2021-01-01</SimulationStart>
  <SimulationEnd>2021-12-31</SimulationEnd>
  <SimID>xToxicLoad-Test</SimID>
  <NumberMC>1</NumberMC>
  <ParallelProcesses>1</ParallelProcesses>
</Parameters>
```

*Template.xrun* files included in the xToxicLoad repository contain comments describing the constraints and purpose of each XML element.

## mc.xml

This file structures information for each Monte Carlo run of xToxicLoad, and most information in this file should not be modified. However, xToxicLoad currently defines two xCropProtection parameters in this file: `OutputApplicationType` and `ProductDatabase`.

`OutputApplicationType` sets the output type of xCropProtection to either product or active substance and `ProductDatabase` provides the file path to the SQLite database containing product formulation information.

Note the different combinations of input (specified in PPM Calendars) and `OutputApplicationType`.

``` { .yaml .no-copy }
input product 			-> output product 			: valid
input product 			-> output product			: valid
input active substance 	-> output active substance	: valid
input active substance 	-> output product 			: invalid
```

This file also defines which columns in the substance and product properties table will be used in the xToxicLoad component.

``` xml
<ToxicLoad module="components" class="ToxicLoad">
    <Pec>
        <FromOutput component="InFieldExposure" output="Pec"/>
    </Pec>
    <LD50>
        <FromOutput component="SubstanceProperties" output="Endpoint"/>
    </LD50>
</ToxicLoad>
```

The name of the column defined in the output attribute of `FromOutput` will be used to calculate the LD50. More than one column may be used in the LD50 calculation by adding additional `FromOutput` elements.

## Substance and product properties.xlsx

The substance and product properies file contains phisio-chemial and ecotoxicity properties for substances.

## xCropProtection.xml

## Landscape scenario

## Steps to create a new scenario