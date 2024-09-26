# Version 1.x

The first major release (version 1.x) implements key goals as summarised the [Introduction][Today-need for a model]. The design is based on *Component-Base-Software-Engineering* (CBSE). So, xLandscape is not a model but a framework to build models, with a core functionality for numeric, multidimensional landscape modelling.  

**xLandscape major entities**:

1. **Core**: inspired by microkernel architecture in CBSE context. Represents key features of the modular landscape modelling approach. *Components* are connected to the core and controlled by the core (necessary minimum). Provides a multidimensional data store. Organises model inputs.
1. **Components**: colloquial the modules of the modular approach. Represent the actual funtionality of a landscape model. Can be quite simple (eg, estimation of water temperature from air) or quite complex (eg, calculating substance transport in streams). Technically precise, *components* are build from *wrapping* scientific models (called 'the module of a component').
1. **xLandscape Models**: an applicable landscape model for a specific purpose. The composition of *components* and the *core* ([Example xLandscape Models](../xLandscape/xLandscape-models.md)). 

<img src="../img/xLandscape - moduls core models.png" alt="xLandscape - Modules, Core, Models" width="900"/>  

*Illustration of the xLandscape ecosystem: components, Core, Models, as well as 'Analysis&Reporting Elements'*  

**xLandscape Characteristics**:

1. **Numeric approach** that works with discretised entities: time is discretised in time steps (any step possible, 'hour' and 'day' are typical in different processes). Spatial entities can be eg, vector polygons or raster cells. This makes xLandscape a spatiotemporally explicit model.
1. **Explicit scales**: phenomenons like variability are assigned to specific scales. Eg, variability of spray-drift deposition might be observed on a *field*-scale. Likewise, explicit *scales* serve as important units in the analysis of landscape modelling outcome, eg. to provide endpoints that fit to the definition of [Specific Protection Goals](https://www.efsa.europa.eu/en/efsajournal/pub/1821).
1. **Monte Carlo**: variability (and uncertainty) are represented by Probability Density Functions (PDFs). This, together with the spatiotemporally explicit approach, provides the functionality to propagate variability of landscape processes, activities and dynamics to landscape model outputs.  
1. **Multidimensional data storage**: Environmental characteristics, agriculture, PPP use, exposure, effects and their attributes, space and time, make xLandscape a multidimensional approach. These data are stored in a  multidimensional storage. Currently, the Hierarchical Data Format ([HDF](https://www.hdfgroup.org/)) is used. At the end of a xLandscape-based model simulation all data resides in the HDF store.
1. **Semantics**: xLandscape introduces *semantics* to improve meaning of data. This is done in a stepwise way. Currently, values have a unit and scale assigned.
1. **Sequential processing**: in version 1.x *components* are executed in a sequential order.
1. **'xcopy' distribution**: an xLandscape-based model can be copied (downloaded) and used without installation. The xLandscape *core* comes with its Python environment and each *component* with their required runtime environment.
1. **Scalability**: basically, the spatial and temporal extent, as well as other simulation characteristics (eg, the number and detail of endpoints) are only limited by computing ressources. Scaleability is a central requirement, also to the design of *components*. Ideally, processes should show a linear scaling behaviour. Besides actual landscape models build with xLandscape, the related analysis software need to cope with (large) raw data volumes typically generated.
1. **Scenarios**: each specific model built with the xLandscape approach has its specific scenario requirements. As long as data requirements can be fulfilled, scenarios of any (global) region and any time period can be used as model input. Scenarios can be of any spatial shape. See also [scenarios](../reference/glossary.md#scenario) in the [Glossary](../reference/glossary.md).
1. **Analysis- and Reporting Elements**: example analysis code and outputs (eg, tables, graphics) are prepared. Typically, [Jupyter](https://jupyter.org/) notebooks are used, each focusing on a certain analysis topic.

## Implementation

The xLandscape *core* and *components* building software are written in **Python**. This language was choosen for its properties, popularity and ease to learn. However, compute demanding processes can be written in basically any language (eg, C, C++, Go) and be integrated as Python packages.  
The inner model of *components* can be written basically in any language. The *component* building process wraps such software, typically including the software (model) specific runtime environment.  

## Core

The modular approach of xLandscape does not intend to loosely couple models. There is a 'framing' element necessary to represent characteristics that make a landscape model according to the use context, goals and requirements (see [Intro](../xLandscape/xLandscape-intro.md)).  
The '*core* and *component*' design was inspired by microkernel architecture in CBSE context. Represents key features of the modular landscape modelling approach.  
Key *core* functionality and characteristics:
1. *Components* are connected to the core
1. *Components* are controlled by the core (necessary minimum: initialisation, data exchange, status request, resource control)
1. Provides a multidimensional data store
1. Semantics
1. External data (scenarios) input
1. xxx

This is illustrated as the blue **'L'** together with the light blue background in xLandscape model schemes:  

<img src="../img/core illustration.png" alt="xlandscape Core Illustration" width="300"/>  

*xlandscape core illustration*


### Propagation of Variability


<img src="../img/variability propagation.png" alt="Propagation of Variability" width="900"/>  

*Propagation of landscape system variability to variability of model predictions*

**Real-world variability has structure**, it is not purely random. 

<img src="../img/variability propagation 2.png" alt="Propagation of Variability" width="1000"/>  

*Real-world variability has structure*


## Modules and Components

You will read the term ***component*** quite often in the context of *xLandscape* and so *xCP*.  = Mo-Based Software
[*components*](#modules-and-components)  
early module: [xDrift](../xLandscape/xLandscape-components.md#xdrift).

## Multidimensional Data Store

currently, [HDF](xLandscape/xLandscape-intro.md#multidimensional-data-store) is being used.  

## Sequential Processing

At version 1.x, xLandscape has a linear processing sequence

<img src="../img/xAquatic linear processing sequence.png" alt="xAquatic" width="900"/>  

*Example sequential processing in xAquatic (status date: xAquatic 2022)*

## Semantics

## Model Input (Geo)Data

## Analysis

### Jupyter notebooks

### Dashboards

### GIS

## Development and User Level


<img src="../img/development and user level.png" alt="Development and User Levels" width="950"/>  


*Development and User Levels (status date: 2022)*


[Today-need for a model]: ../xLandscape/xLandscape-intro.md#today---applicable-landscape-models-needed