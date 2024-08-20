# Distributions

Some elements of xCropProtection can be parameterized with probability distributions. When a probability distribution is defined, the distribution is sampled every time an application occurs. Elements which support probability distributions are:

- `Indications`
- `Indication`
- `ApplicationRate`
- `InCropBuffer`
- `InFieldMargin`
- `MinimumAppliedArea`

## Uniform distribution

This defines a numeric distribution with an arbitrary outcome between *a* and *b* where each outcome is equally likely. *a* and *b* are the minimum and maximum values, respectively. Users define the bounds of a uniform distribution with the following steps:

- Define the element's type as "xCropProtection.UniformDistribution"
- Add a child element `Lower`, which defines the minimum value of the distribution
    - type="float"
    - scales="global"
- Add a child element `Upper`, which defines the maximum value of the distribution
    - type="float"
    - scales="global"

Example:

``` xml
<ApplicationRate type="xCropProtection.UniformDistribution" unit="g/ha" scales="time/year, space/base_geometry">
    <Lower type="float" scales="global">50</Lower>
    <Upper type="float" scales="global">75</Upper> 
</ApplicationRate>
```

Every time an application occurs, xCropProtection will choose a value for `ApplicationRate` between 50 and 75 following the rules of uniform distributions.

Elements which may use this distribution are:

- `ApplicationRate`
- `InCropBuffer`
- `InFieldMargin`
- `MinimumAppliedArea`

## Discrete uniform distribution

This defines a numeric distribution with an arbitrary outcome between *a* and *b* where a finite number of outcomes are equally likely. *a* and *b* are the minimum and maximum values, respectively. Users define the bounds of a discrete uniform distribution with the following steps:

- Define the element's type as "xCropProtection.DiscreteUniformDistribution"
- Add a child element `Lower`, which defines the minimum value of the distribution
    - type="float"
    - scales="global"
- Add a child element `Upper`, which defines the maximum value of the distribution
    - type="float"
    - scales="global"

Example:

``` xml
<InCropBuffer type="xCropProtection.DiscreteUniformDistribution" unit="m" scales="time/year, space/base_geometry">
    <Lower type="float" scales="global">0</Lower>
    <Upper type="float" scales="global">10</Upper> 
</InCropBuffer>
```

Every time an application occurs, xCropProtection will choose a value for that application's `InCropBuffer` between 0 and 10 following the rules of discrete uniform distributions.

Elements which may use this distribution are:

- `ApplicationRate`
- `InCropBuffer`
- `InFieldMargin`
- `MinimumAppliedArea`

## Normal distribution

This defines a continuous bell-shaped probability distribution of numeric values. It is symmetrical about its mean (*μ*) and most values cluster around the center of the range. Users define the parameters of a normal distribution with the following steps:

- Define the element's type as "xCropProtection.NormalDistribution"
- Add a child element `Mean`, which defines the mean value of the distribution
    - type="float"
    - scales="global"
- Add a child element `SD`, which defines the standard deviation of the distribution
    - type="float"
    - scales="global"

Example:

``` xml
<ApplicationRate type="xCropProtection.NormalDistribution" unit="g/ha" scales="time/year, space/base_geometry">
    <Mean type="float" scales="global">50</Mean>
    <SD type="float" scales="global">4.5</SD> 
</ApplicationRate>
```

Every time an application occurs, xCropProtection will choose a value for `ApplicationRate` following the rules of uniform distributions (with a mean of 50 and a standard deviation of 4.5).

Elements which may use this distribution are:

- `ApplicationRate`
- `InCropBuffer`
- `InFieldMargin`
- `MinimumAppliedArea`

## Choice distribution

This represents a distribution over a set of objects. Each object has an associated probability that determines how likely that object will be selected compared to any other objects. All probabilities must sum to 1.0. Users define the parameters of a choice distribution with the following steps:

- Define the element's type as "xCropProtection.ChoiceDistribution"
- Create one or more child elements that represent possible choices
    - probability="*x*" where 0 ≤ *x* ≤  1

Example:

``` xml
<Indication type="xCropProtection.ChoiceDistribution" scales="time/year, space/base_geometry">
    <ApplicationSequence probability="1">
        ...
    </ApplicationSequence>
    <ApplicationSequence probability="1">
        ...
    </ApplicationSequence>
    <ApplicationSequence probability="1">
        ...
    </ApplicationSequence>
```

Elements which may use this distribution are:

- `Indications`
    - Child element: `Indication`
- `Indication`
    - Child element: `ApplicationSequence`