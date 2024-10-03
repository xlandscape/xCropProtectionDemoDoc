# xToxicLoad

xToxicLoad is a Landscape Model that calculates simple toxic load values of pesticides by field and time step (typically by day).  
A *toxic load* represents the multiple of an effect (on a field, at a certain time). It is calculated by deviding the exposure by a defined ecotoxicological endpoint: eg, *ToxicLoad(x,t)* = *PEC(x,t)* / *LD50*. In the example an LD50 is used, however, the ecotox endpoint can be any of interest. A LD50, eg, might represent an oral or contact bee ecotox endpoint.


## Background
At present, intended for demonstration purposes, 