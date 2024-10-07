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

## Applicability

The application of xLandscape framework is not limited to its original key purpose for RA, ie to generate model results for RA endpoints (exposure, effects). xLandscape can be employed for modelling quite a large range of spatiotemporally phenomenon, eg, to model the spatiotemporally occurrence of bee forage (nectar, pollen), the use of pesticides in cultivated landscapes, the toxic loads of chemicals in landscapes, etc.

## Programming Language

The xLandscape *core* and *components* building software are written in **Python**. This language was choosen for its properties, popularity and ease to learn. However, compute demanding processes can be written in basically any language (eg, C, C++, Go) and be integrated as Python packages.  
The inner model of *components* can be written basically in any language. The *component* building process wraps such software, typically including the software (model) specific runtime environment.  
Development is **versioned** and currently done using **Github** ([Github/xLandscape](https://github.com/xlandscape)).

## Core

The modular approach of xLandscape does not intend to loosely couple models. There is a 'framing' element necessary to represent characteristics that make a landscape model according to the use context, goals and requirements (see [Intro](../xLandscape/xLandscape-intro.md)).  
The '*core* and *component*' design was inspired by microkernel architecture in Component-based Software Engineering (CBSE) context. Represents key features of the modular landscape modelling approach.  
Key *core* functionality and characteristics:

1. The *core* provides the (Python) **framework to build *components*** (eg, interfaces for data exchange, data semantics, initialisation, control, *component* self-description, status request)
1. The *core* provides the **framework to build compositions**, ie actual landscape models (currently implemented as XML)
1. The *core* provides the **framework for a 'semantic context'** that enables operating with explicit entities (eg, scales) and assures inner landscape model data **consistency**
1. The *core* provides the **framework for operating with multidimensional data**
1. The *core* provides functionality for landscape **simulation control, status observer, ressources and logging**
1. The *core* provides functionality for reading the ***parameterisation*** and ***configuration*** of a Landscape Model as defined by the user

This is illustrated as the blue **'L'** together with the light blue background in xLandscape model schemes:  

<img src="../img/core illustration.png" alt="xlandscape Core Illustration" width="300"/>  

*xlandscape core illustration*

## Components

Essentially all **functionality is represented by *components***.  
*Components* are initiated by and operated in the framework of the *core*. A composition of the *core* and *components* make a Landscape Model.  
*Components* can contain and represent basically any simulation model, eg,

- (Large) **Mechanistic models**, eg, simulating substance exposure, fate and effects (eg, PRZM, PEARL, Macro, Cascade-Toxswa, GUTS, Mastep, Streamcom)
- **Data-driven models**, eg, representing variability of spray-drift deposition (eg, [xDrift](../xLandscape/xLandscape-components.md#xdrift), AgDrift), results from ecotoxicologial studies (eg, Dose-response, Species Sensitivity Distributions, Toxic-Load), or lookup tables (eg, bee forage production by vegetation and time)
- **Hybrid models**, eg, for simulating residues of substances in plants and commodities
- Models simulating **agricultural management**, eg, **PPP use** (eg, [xCropProtection](../xLandscape/xLandscape-components.md#xcropprotection))
- **Small calculations**, eg for modelling specific environmental conditions (eg, sunshine hours, water temperature)
- **(Geo)data inputs**: external data is imported into a Landscape Model using specific *components*, eg, weather, land use, or soil data. Besides such explicit data inputs. This applies, eg, when complex mechanistic models bring some default settings with them which are loaded using text-files.
- **Analysis**: when a simulation is done it might be nice to see some analysis automatically. So, *components* can be build and integrated into a Landscape Model for analysis purposes

> Colloquially, we might call the pieces of a modular Landscape Model *modules*, eg say *'xDrift is a module in the xAquatic landscape model'*, or *'in which repository can I find the module for PPP use?'*.  
However, following the terminology of Component-Based-Software-Engineering (CBSE), we need to be more precise and talk about *components*. A *component* contains a *model* which is also called a *module*. *Models* (*modules*) represent the actual functionality.  
A *model* (*module*) becomes a xLandscape *component* when it is wrapped using the xLandscape *core* framework.

The graphic below shows the design of a *component*:  

<img src="../img/Component - stream temperature.png" alt="xlandscape" width="300"/>  

*Component 'Stream_Temperature' representing a model to estimate stream temperature (T_stream) from air temperature (T_air). (a blue background indicates connection to an internal source (semantically enriched), whereas a grey background represents connection to external sources; the diamond represents the actual model ('module'))*

A *component* has the following elements: 

1. **Input**: the data input to be processed by the *component*. Inputs can be connected to external data sources (eg, files, data bases, APIs) (grey background) or to the internal *multidimensional store* (blue background)
1. **Init/Control**: inputs for the initialisation and control of a *component* and its *module* (*model*). Init/Control can come from  external data sources (eg, xml/text files) (grey background) or from the internal *multidimensional store* (blue background)
1. **Output**: the data output of a *component*. Outputs are typically written to the internal *multidimensional store* (blue background) yet, can also be written to external data storages (eg, Relational Database Management Systems, files, cloud storage) (grey background)
1. **Module (model)**: the actual *model* (*module*) that provides the functionality, ie, conducts the simulation (blue diamond element)
  
All internal data (information) is semantically-enriched (see [Semantics](#semantics)).  
*Components* typically have multiple in- and outputs.  
Example *components* are introduced in section [Components](../xLandscape/xLandscape-components.md).  


## Landscape Model Composition

**A composition of *components* and the *core* builds a landscape model.** [Example Landscape Models](../xLandscape/xLandscape-models.md) built are [xAquatic](../xLandscape/xLandscape-models.md#xaquatic-invertebrates), to simulate exposure and effects of aquatic organisms in catchments, [xOff-Field-Soil](../xLandscape/xLandscape-models.md#xofffieldsoil), to calculate exposure of soil organisms living next to fields, or [xPollinator](../xLandscape/xLandscape-models.md#xpollinator) to simulate nectar and pollen occurrence for building bee modelling scenarios.

The graphic below shows the composition of a very simple Landscape Model that inputs a stream network, together with weather data, in order to calculate stream temperature:

- The model is built using **2 *components***: 'Weather_MARS' inputs (external) weather data (from the EU 'MARS' database) and writes defined data (eg, air temperature, T_air) into the landscape model storage, whereas *component* 'Stream_Temperature' takes T_air from the store and transfers this to an estimated stream temperature (T_stream) using a model.
- The **blue 'L' represents the xLandscape [*core*](#core)**. The light blue rectancle-shaped background represents the semantically-enriched space of this specific model (eg, T_air is defined with a unit and assigned spatial and temporal scales; T_air is consistantly available to all *components* of the model).
- The Landscape Model is **parameterised using an XML file** (eg, to define the landscape scenario and simulation time period; grey box)
- Typical landscape model input data (green box) comprises land use/cover, weather, habitats and pesticide use, yet, depends on the landscape model.
- The ***Data Storage*** contains all data defined by the landscape model designer, as relevant to the landscape model application (inputs, interim, and model outputs). Thus, the *Data Storage* can be recognised as representing *'the landscape'* from the view of the model purpose. Eg, [xAquatic](../xLandscape/xLandscape-models.md#xaquatic-invertebrates) stores data on land use, weather, hydrology, PPP use, stream exposure and effects on aquatic invertegrates, whereas [xPollinator](../xLandscape/xLandscape-models.md#xpollinator) outputs stores nectar and pollen occurrence by space and time. 


<img src="../img/xLandscape model building scheme.png" alt="xlandscape" width="1000"/>  

*Illustration of a simple Landscape Model, built from 2 *components* (Weather_MARS, Stream_Temperature) and the xlandscape core*


### Propagation of Variability


<img src="../img/variability propagation 1a.png" alt="Propagation of Variability" width="900"/>  

*Propagation of landscape system variability to variability of model predictions*

**Real-world variability has structure**, it is not purely random. 

<img src="../img/variability propagation 2.png" alt="Propagation of Variability" width="1000"/>  

*Real-world variability has structure*


## Modules and Components

You will read the term ***component*** quite often in the context of *xLandscape* and so *xCP*.  = Mo-Based Software
[*components*](#modules-and-components)  
early module: [xDrift](../xLandscape/xLandscape-components.md#xdrift).

## Multidimensional Data Store - *'The Landscape'*


represents 'the landscape', ie such data that is defined (by model design and configuration) to be input or generated, representing the landscape information that is inteded to be kept for the model purpose (outcome)  

might ask *'what is actually the landscape in your landscape model'*  
> There is only those data in the data store that is required by the modelling purposes and defined valuable for analysis by the user  

the *multidimensional store* provides the landscape 'status' (eg, including the parameterisation and configuration)

currently, [HDF](xLandscape/xLandscape-intro.md#multidimensional-data-store) is being used.  

<img src="../img/multidimensional data store HDF.png" alt="Multidimensional Data Store" width="880"/>  

*Multidimensional Data Store xxx*

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

## Technical Implementation