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
1. **Explicit representation of scales**: phenomenons like variability are assigned to specific scales. Eg, variability of wind direction, as defined in a is 
1. Multidimensional data storage
1. Monte Carlo
1. Variability propagation ... Probability Density Functions (PDFs)
1. **Semantics**: 
1. Analysis- and Reporting Elements
1. Sequential processing



- numeric, Monte Carlo
- multidimensional,
- Python
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
