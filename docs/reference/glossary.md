# Glossary
Basically, all xCP entities are defined close to the real-world objects they represent.  
(September 2024: status=work in progress; during development, 'xxx' marks sections to be done)
<br>

## Active Substance (a.s.)
An active substance in a plant protection product is any chemical, plant extract, pheromone, or micro-organism (including viruses) that acts against pests or affects plants, parts of plants, or plant products (https://food.ec.europa.eu/plants/pesticides_en). Essentially, it's the component that provides the intended protective or pesticidal effect.  
*Active Substances* have physical and chemical properties as well as ecotoxicological endpoints. These data are kept in corresponding databases. 

## Application
When a PPP is/PPPs are applied to a certain crop at a certain field we call this an *Application*. Typically, a farmer puts a PPP (or a set of PPPs) into a spraying tank, fills the tank up with water, drives to the field and sprays the solution onto the field (into the crop). In xCP context, the term *Application* is used close to agricultural practice, yet, is related to its use in pesticide risk assessment, especially the exposure modelling part.  
 An *Application* is defined by  
 - the PPP (or PPPs) to be applied  
 - an *Application Rate* (eg, in [µg a.s./ha] or [mL PPP/ha])  
 - a time when the application is intended (eg, deterministic day or a time window with a related distribution function)  
 - the technology with which the application will be done (eg, boom sprayer)  
 - risk mitigation measures (eg, spray buffer, in-crop buffer, drift-reducing nozzles)  
<br>

![Application](../img/sprayApplication.jpg "PPP Spray Application using a boom sprayer")  
*PPP spray application using a boom sprayer*  

Remark: Influenced by classic exposure modelling, at the current development status, the definition of an *Application* includes the definition of an application timing, although in agricultural practice typically the use of a PPP is related to crop development stages. Thus, currently, the modeller has to determine the dependence of regional crop development with time. Future xCP versions are planned to allow defining an *Application* related to crop development stage (which can be provided by databases or crop development modelling). 


## Application Rate
In agricultural practice, the amount of PPPs applied to a field is usually determined as amount PPP by field area. 
The farmer typically determines the volume PPP [mL] by field area [ha] (eg, considering the crop development status, *'the higher the crop the more PPP needed'*).   
As risk assessment often focuses on active substance (a.s.), so does modelling. Therefore, in xCP the *Application Rate* can be defined as amount a.s. or PPP per field ares (eg, [µg a.s./ha], [mL PPP/ha]).

## Application Sequence
A sequence of individual PPP *Applications*. Each individual *Application* within an *Application Sequence* can be defined independently. Thus, an *Application Sequence* can represent, eg, the multiple use of the same PPP (PPPs) using the same technology and risk mitigation, yet, at individual application rates (eg, as often the case for fungicide uses in orchards). However, an *Application Sequence* can also represent uses of different PPPs in a sequence (as illustrated in the graphic below).   

![Illustration of a PPP application sequence using different PPPs](../img/PPP%20application%20sequence%20using%20different%20PPPs.png)
*Illustration of a PPP application sequence using different PPPs*  
(https://rwz.ag/fileadmin2023/Agrarhandel/Weinbau/Mosel/240124_bild_weinbauempfehlung-pflanzenschutz-mosel.png)

## Application Window
 The time when an application is planned to be conducted. In a modelling experiment using xCP, an *Application Window* can be a deterministic day or a time span (eg, 1.-14. April). In the latter case, a probability distribution function is assigned to an application window from which actual application dates are sampled during model runtime. 

Remark: Influenced by classic exposure modelling, at the current development status, the definition of an *Application* includes the definition of an application timing (*Application Window*), although in agricultural practice typically the use of a PPP is related to crop development stages. Thus, currently, the modeller has to determine the dependence of regional crop development with time. Future xCP versions are planned to allow defining an *Application* related to crop development stage (which can bw provided by databases or crop development modelling).  
Also, typically farmers' decisions depend on agricultural and environmental conditions. xCP is planned to allow the definition of such dependency rules, eg, not to conduct a certain spray application when a rainstorm is predicted by weather forecast.  

## Buffer
A distance ([m]) that is kept (has to be kept) to a certain entity during an agricultural activity. Buffers are typically used to implement risk mitigation means, eg, to reduce spray-drift depositions into habitats of non-target-organisms. To protect aquatic organisms no-spray buffers are defined as distance to water bodies (eg, a PPP is allowed to be spray no closer than 10 m distance to streams). To protect terrestric organisms, often in-field or in-crop buffers are defined (eg, spraying has to keep a 5 m distance from the cropped/field boundery).

## Experiment
The term *Experiment* has been introduced to [xLandscape](../xLandscape/xLandscape-intro.md#xlandscape) model simulations as an analogue to experimental setups.  
An *Experiment* has a single model parameterisation (including xCP parameterisation) and consists of a number of *Monte Carlo* runs. The latter are independent from each other, ie. in each *Monte Carlo Run* the defined variabilities (Probability Density Functions, PDFs) are independently sampled.  
As compared to experimental setups, the 'control' setup is basically assumed to be the no-PPP use, ie non-exposure situation. However, alternative baseline scenarios can be defined as separate *Experiments* (eg, representing alternative/'organic'/'biological' pest control measures) and their outcome considered in the (comparative) analysis.  

## In-/Off-field, In-/Off-crop
In regulatory risk assessment in Europe, protection goals and risk assessment approaches are different for in-field and off-field areas. Basically, the **in-field area** is given by the property of the farmer and its bounderies (as you might find on cadastral maps). In cultivated landscapes, **off-field areas** are typically represented by parts of the field margin (eg, between roads and fields), riparian zones, wood margins. When you see vegetation strips between two arable fields, these are caused due to the working space of the agricultural machinery but  do not represent off-field areas as the two arable properties directly border to each other.  
**In-crop** simply represents the currently cropped area. Likewise, **off-crop** represents all (currently) non-cropped area.  
**In-field off-crop** areas are such within the field (property) of a farmer, yet, are currently not cropped. Such areas occur as (in-field) field margins, in some cases just left as a fallow strip, in others of sown flowering strip (to support wildlife and forage for insects). Such in-field margins are also intended to reduce potential run-off of pesticide residues from the field into off-field areas and streams.  

<img src="../img/3a%20Off-Field%20Soil%20Risk%20Figure_1.png" width="800" height="250">  

*Illustration of In-/Off-Field vs. In-/Off-Crop definition. The scheme on the left shows the definition as occurring in official documents. The image on the right shows a typical field situation (Hessian, Germany)*  
<br>
<img src="../img/in-crop%20off-crop%20illustration.png" width="350" height="200">  
*Illustration of In-/Off-Field vs. In-/Off-Crop using a schematic scenario. The in-field (left part) is cropped (brown color), yet, has an in-field off-crop margin (light green). The off-field area (right part) is divided into two zones, representing two different land cover types in the expample (wood margin, wood core)*

## In-crop Buffer
As a *Risk Mitigation* option, typically to reduce spray-drift depositions into off-field areas, in-crop buffer represent a zone (distance [m]) from the cropped area boundery which must not be sprayed with the PPP of such a label instruction.  
<br>
<img src="../img/Illustration of in-crop buffer.png" width="350" height="200">  
*Illustration of In-/Off-Field vs. In-/Off-Crop using a schematic scenario. The in-field (left part) is cropped (brown color), yet, has an in-field off-crop margin (light green) as well as an in-crop buffer (solid box). The cropped area within the in-crop buffer is allowed to be sprayed (solid box), whereas the cropped area outside is not. The off-field area (right part) is divided into two zones, representing two different land cover types in the expample (wood margin, wood core)*

## Indication
Generally, measures to protect plants (crop) from a certain pest.  
In xCP, an *Indication* is an explicit part of its parameterisation. An *Indication* is made of *PPP Application Sequences*, at minimum one *PPP Application Sequence*. If more than one *Application Sequence* is defined in an *Indication*, these sequences are considered **alternative** *Application sequences* ('OR' related). Thus, the xCP parameterisation entity *Indication* can be used to define alternative PPP use pattern, eg, reflecting product market shares or fractions 'biological' or 'organic' pest control means.  
Multiple *Indications* can be defined in an xCP parameterisation, as many as necessary to represent a simple or complex real-world PPP use pattern in one or many crops. Each individual *Indication* defined will be conducted in an xCP simulation. 

![xCP Entities and their Relationship](../img/xCP%20entities%20and%20their%20relationship.png "xCP Entities and their Relationship")  
*xCP entities and their relationship xxx to be replaced by final img*

## Monte Carlo Run
Monte Carlo simulations rely on random sampling to obtain numerical results. 
Monte Carlo methods are mainly used in three distinct problem classes: optimization, numerical integration, and generating draws from a probability distribution. They can also be used to model phenomena with significant uncertainty in inputs, such as calculating the risk of a nuclear power plant failure. Monte Carlo methods are often implemented using computer simulations, and they can provide approximate solutions to problems that are otherwise intractable or too complex to analyze mathematically.

[xLandscape](../xLandscape/xLandscape-intro.md#xlandscape) is a numerical model  



## Plant Protection Calender xxx
  
the origin
driven by crop protection advisory services as well as the practice of farmers

can be defined for an entire modelling simulation (experiment)  
![Example Plant Protection Calender](../img/Example%20plant%20protection%20recommendation%20in%20apples.jpg "Example Plant Protection Recommendation in Apple")  
*Example Plant Protection Recommendation in Apple*


## Plant Protection Measure (PPM)
An action to prevent or control pests, eg, protecting apples against powdery mildew fungy or protecting olives against the white fly.  
In xCP, a *Plant Protection Measure* is represented by one or more *Indications*.  

## Plant Protection Product (PPP)
Plant protection products (PPPs) are chemical or biological products which are used to protect plants or plant products from harm caused by animals (eg, insects and rodents) or diseases such as fungal infestation. Products which are used to eliminate unwanted field weeds are also considered PPPs. The term “pesticides” is often used instead of plant protection product.  
PPPs contain one or more *Active Substances* and other co-formulants (substances which are supposed to have a positive effect on the production, storage or use of a product). The product itself is used in various forms, for example as spraying agents for seed treatment or in granular form.  


## Risk Mitigation / Risk Mitigation Measures
Regarding the use of PPPs and from an operational point of view, here *Risk Mitigation* basically refers to reducing exposure caused by PPP application. For more information have a look into the outcome of the [MAgPie Workshop](https://www.openagrar.de/receive/openagrar_mods_00027102 "Mitigating risks of Plant Protection Products in the environment").
  
In xCP, currently the following *Risk Mitigation* measures are implemented:
- no-spray buffer (typically defined in relation to water bodies)
- in-crop buffer (a distance a farmer has to keep from the cropped boundery when spraying)
- use of drift-reducing nozzles (sprayer technology to reduce drift)

## Scenario xxx
In general, a scenario represents a certain status of the driving conditions of a xxx. 

the term becomes precise when adding context  
PPP use scenario  
landscape scenario

## Simulation
The term *Simulation* is not precisely defined and is used somehow colloquial with different meanings. This is not a problem as the actual meaning typically gets clear in its use context:  
- a model simulation can just mean to parameterise and run a model in general
- an xLandscape model simulation can mean to conduct an *Experiment*, ie, here the terms are used synonymously
- a *Simulation* can also address an individual *Monte Carlo* run of an xLandscape model [*Experiment*](#experiment-v01). 

