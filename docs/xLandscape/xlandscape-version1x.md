# xLandscape Version 1.x

The first major release (version 1.x) implements key goals as summarised the [Introduction](../xLandscape/xLandscape-intro.md#today---we-need-an-applicable-product). The design is based on *Component-Base-Software-Engineering* (CBSE). So, xLandscape is not a model but a framework to build models, with a core functionality for numeric, multidimensional landscape modelling.  
**Main entities**:

1. **Core**: inspired by microkernel architecture in CBSE context. Represents key features of the modular landscape modelling approach. *Components* are connected to the core and controlled by the core (necessary minimum). Provides a multidimensional data store. Organises model inputs.
1. **Components**: colloquial the modules of the modular approach. Represent the actual funtionality of a landscape model. Can be quite simple (eg, estimation of water temperature from air) or quite complex (eg, calculating substance transport in streams). Technically precise, *components* are build from *wrapping* scientific models (called 'the module of a component').
1. **xLandscape Models**: an applicable landscape model for a specific purpose. The composition of *components* and the *core* ([Example xLandscape Models](../xLandscape/xLandscape-models.md)). 

<img src="../img/xLandscape - moduls core models.png" alt="xLandscape - Modules, Core, Models" width="900"/>  

*Illustration of the xLandscape ecosystem: components, Core, Models, as well as 'Analysis&Reporting Elements'*  

**Characteristics**:

1. **Numeric approach** that works with discretised entities: time is discretised in time steps (any step possible, 'hour' and 'day' are typical in different processes). Spatial entities can be eg, vector polygons or raster cells. This makes xLandscape a spatiotemporally explicit model.
1. **Explicit representation of scales**: phenomenons like variability are assigned to specific scales. Eg, variability of spray-drift deposition might be observed on a *field*-scale. Likewise, explicit *scales* serve as important units in the analysis of landscape modelling outcome, eg. to provide endpoints that fit to the definition of [Specific Protection Goals](https://www.efsa.europa.eu/en/efsajournal/pub/1821).
1. **Monte Carlo**: variability (and uncertainty) are represented by Probability Density Functions (PDFs). This, together with the spatiotemporally explicit approach, provides the functionality to propagate variability of landscape processes, activities and dynamics to landscape model outputs.  
1. **Multidimensional data storage**: Environmental characteristics, agriculture, PPP use, exposure, effects and their attributes, space and time, make xLandscape a multidimensional approach. These data are stored in a  multidimensional storage. Currently, the Hierarchical Data Format ([HDF](https://www.hdfgroup.org/)) is used. At the end of a xLandscape-based model simulation all data resides in the HDF store.
1. **Semantics**: xLandscape introduces *semantics* to improve meaning of data. This is done in a stepwise way. Currently, values have a unit and scale assigned.
1. **Sequential processing**: in version 1.x *components* are executed in a sequential order.
1. **Analysis- and Reporting Elements**: example analysis code and outputs (eg, tables, graphics) are prepared. Typically, [Jupyter](https://jupyter.org/) notebooks are used, each focusing on a certain analysis topic.
1. **'xcopy' distribution**: an xLandscape-based model can be copied (downloaded) and used without installation. The xLandscape *core* comes with its Python environment and each *component* with their required runtime environment.
1. **Scalability**: basically, the spatial and temporal extent, as well as other simulation characteristics (eg, the number and detail of endpoints) are only limited by computing ressources. 
1. **Scenarios**: xxx Scenarios can be of any spatial shape.  [scenarios](../reference/glossary.md#scenario)

The xLandscape *core* and building *components* software are written in Python
early module: xDrift (ref)  


## Core


## Modules and Components

You will read the term ***component*** quite often in the context of *xLandscape* and so *xCP*.  = Mo-Based Software
[*components*](#modules-and-components) 
lego bricks

## Multidimensional Data Store

currently, [HDF](xLandscape/xLandscape-intro.md#multidimensional-data-store) is being used.  

## Sequencial Processing

At version 1.x, xLandscape has a linear processing sequence

<img src="../img/xAquatic linear processing sequence.png" alt="xAquatic" width="900"/>  


*Example sequential processing in xAquatic (status date: xAquatic 2022)*

## Model Input (Geo)Data

## Analysis

### Jupyter notebooks

### Dashboards

### GIS
