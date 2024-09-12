# Glossary
Basically, all xCP entities are defined close to the real-world objects they represent.  
(September 2024: status=work in progress; during development, 'xxx' mark locations to be done, 'v0x' mark sections of draft level)
<br>

## Active Substance (a.s.) (v01)
An active substance in a plant protection product is any chemical, plant extract, pheromone, or micro-organism (including viruses) that acts against pests or affects plants, parts of plants, or plant products (https://food.ec.europa.eu/plants/pesticides_en). Essentially, it's the component that provides the intended protective or pesticidal effect.

## Application (v01)
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


## Application Rate (v01)
In agricultural practice, the amount of PPPs applied to a field is usually determined as amount PPP by field area. 
The farmer typically determines the volume PPP [mL] by field area [ha] (eg, considering the crop development status, *'the higher the crop the more PPP needed'*).   
As risk assessment often focuses on active substance (a.s.), so does modelling. Therefore, in xCP the *Application Rate* can be defined as amount a.s. or PPP per field ares (eg, [µg a.s./ha], [mL PPP/ha]).

## Application Sequence (v01)
A sequence of individual PPP *Applications*. Each individual *Application* within an *Application Sequence* can be defined independently. Thus, an *Application Sequence* can represent, eg, the multiple use of the same PPP (PPPs) using the same technology and risk mitigation, yet, at individual application rates (eg, as often the case for fungicide uses in orchards). However, an *Application Sequence* can also represent uses of different PPPs in a sequence (as illustrated in the graphic below).   

![Illustration of a PPP application sequence using different PPPs](../img/PPP%20application%20sequence%20using%20different%20PPPs.png)
*Illustration of a PPP application sequence using different PPPs*  
(https://rwz.ag/fileadmin2023/Agrarhandel/Weinbau/Mosel/240124_bild_weinbauempfehlung-pflanzenschutz-mosel.png)

## Application Window (v01)
 The time when an application is planned to be conducted. In a modelling experiment using xCP, an *Application Window* can be a deterministic day or a time span (eg, 1.-14. April). In the latter case, a probability distribution function is assigned to an application window from which actual application dates are sampled during model runtime. 

Remark: Influenced by classic exposure modelling, at the current development status, the definition of an *Application* includes the definition of an application timing (*Application Window*), although in agricultural practice typically the use of a PPP is related to crop development stages. Thus, currently, the modeller has to determine the dependence of regional crop development with time. Future xCP versions are planned to allow defining an *Application* related to crop development stage (which can bw provided by databases or crop development modelling).  
Also, typically farmers' decisions depend on agricultural and environmental conditions. xCP is planned to allow the definition of such dependency rules, eg, not to conduct a certain spray application when a rainstorm is predicted by weather forecast.  

## Buffer (v01)
A distance ([m]) that is kept (has to be kept) to a certain entity during an agricultural activity. Buffers are typically used to implement risk mitigation means, eg, to reduce spray-drift depositions into habitats of non-target-organisms. To protect aquatic organisms no-spray buffers are defined as distance to water bodies (eg, a PPP is allowed to be spray no closer than 10 m distance to streams). To protect terrestric organisms, often in-field or in-crop buffers are defined (eg, spraying has to keep a 5 m distance from the cropped/field boundery).

## Ecotox Endpoints

## Experiment 
xxx 
A set of *Monte Carlo Runs*.  
baseline (typically zero exposure, yet can be a alternative pest control measures, eg 'organic')

## In-/Off-field, In-/Off-crop (v01)
In regulatory risk assessment in Europe, protection goals and risk assessment approaches are different for in-field and off-field areas. Basically, the **in-field area** is given by the property of the farmer and its bounderies (as you might find on cadastral maps). In cultivated landscapes, **off-field areas** are typically represented by parts of the field margin (eg, between roads and fields), riparian zones, wood margins. When you see vegetation strips between two arable fields, these are caused due to the working space of the agricultural machinery but  do not represent off-field areas as the two arable properties directly border to each other.  
**In-crop** simply represents the currently cropped area. Likewise, **off-crop** represents all (currently) non-cropped area.  
**In-field off-crop** areas are such within the field (property) of a farmer, yet, are currently not cropped. Such areas occur as (in-field) field margins, in some cases just left as a fallow strip, in others of sown flowering strip (to support wildlife and forage for insects). Such in-field margins are also intended to reduce potential run-off of pesticide residues from the field into off-field areas and streams.  

<img src="../img/3a%20Off-Field%20Soil%20Risk%20Figure_1.png" width="800" height="250">  

*Illustration of In-/Off-Field vs. In-/Off-Crop definition. The scheme on the left shows the definition as occurring in official documents. The image on the right shows a typical field situation (Hessian, Germany)*  
<br>
<img src="../img/in-crop%20off-crop%20illustration.png" width="350" height="200">  
*Illustration of In-/Off-Field vs. In-/Off-Crop using a schematic scenario. The in-field (left part) is cropped (brown color), yet, has an in-field off-crop margin (light green). The off-field area (right part) is divided into two zones, representing two different land cover types in the expample (wood margin, wood core)*


## In-crop Buffer (v01)
As a *Risk Mitigation* option, typically to reduce spray-drift depositions into off-field areas, in-crop buffer represent a zone (distance [m]) from the cropped area boundery which must not be sprayed with the PPP of such a label instruction.  
<br>
<img src="../img/Illustration of in-crop buffer.png" width="350" height="200">  
*Illustration of In-/Off-Field vs. In-/Off-Crop using a schematic scenario. The in-field (left part) is cropped (brown color), yet, has an in-field off-crop margin (light green) as well as an in-crop buffer (solid box). The cropped area within the in-crop buffer is allowed to be sprayed (solid box), whereas the cropped area outside is not. The off-field area (right part) is divided into two zones, representing two different land cover types in the expample (wood margin, wood core)*


## Indication (v01)
Generally, measures to protect plants (crop) from a certain pest.  
In xCP, an *Indication* is an explicit part of its parameterisation. An *Indication* is made of *PPP Application Sequences*, at minimum one *PPP Application Sequence*. If more than one *Application Sequence* is defined in an *Indication*, these sequences are considered **alternative** *Application sequences* ('OR' related). Thus, the xCP parameterisation entity *Indication* can be used to define alternative PPP use pattern, eg, reflecting product market shares or fractions 'biological' or 'organic' pest control means.  
Multiple *Indications* can be defined in an xCP parameterisation, as many as necessary to represent a simple or complex real-world PPP use pattern in one or many crops. Each individual *Indication* defined will be conducted in an xCP simulation. 

![xCP Entities and their Relationship](../img/xCP%20entities%20and%20their%20relationship.png "xCP Entities and their Relationship")  
*xCP entities and their relationship xxx to be replaced by final img*

## Monte Carlo Run


## Plant Protection Calender (PPC)
  
the origin
driven by crop protection advisory services as well as the practice of farmers

can be defined for an entire modelling simulation (experiment)  
![Example Plant Protection Calender](../img/Example%20plant%20protection%20recommendation%20in%20apples.jpg "Example Plant Protection Recommendation in Apple")  
*Example Plant Protection Recommendation in Apple*


## Plant Protection Measure (PPM) (v01)
An action to prevent or control pests, eg, protecting apples against powdery mildew fungy or protecting olives against the white fly.  
In xCP, a *Plant Protection Measure* is represented by one or more *Indications*.  

## Plant Protection Product (PPP) (v01)
Plant protection products (PPPs) are chemical or biological products which are used to protect plants or plant products from harm caused by animals (eg, insects and rodents) or diseases such as fungal infestation. Products which are used to eliminate unwanted field weeds are also considered PPPs. The term “pesticides” is often used instead of plant protection product.  
PPPs contain one or more *Active Substances* and other co-formulants (substances which are supposed to have a positive effect on the production, storage or use of a product). The product itself is used in various forms, for example as spraying agents for seed treatment or in granular form.  


## Risk Mitigation


ref:  
[MAgPie](https://www.openagrar.de/receive/openagrar_mods_00027102)


## Simulation
a model simulation 
compared to *Experiment* 


## Spray-drift Reduction