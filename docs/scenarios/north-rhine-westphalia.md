**In progress**

## Overview

This scenario represents arable land in North Rhine-Westphalia in 2018. The application information is derived from a survey conducted over the time period of 1995-2020 which identifies substances, quantities, and what region applications on crops occurred in.

[GitHub repository for scenario](https://github.com/xlandscape/Scenario-NRW)

## Geo information

The spatial data for this scenario was constructed based on [ATKIS](https://www.adv-online.de/Products/Geotopography/ATKIS/) polygons from 2016. The ATKIS polygons were filtered to only include polygons labeled as arable. A [national scale raster crop type map of Germany](https://zenodo.org/records/10640528) (Schwieder et al.) was used to attribute the ATKIS polygons with more detailed crop types. This was done by summarizing the raster crop map for each polygon and choosing the crop type with the greatest number of raster cells.


## Application information

The source application information was obtained from a survery of growers in Germany conducted from 1995 to 2020. Each row in the source data represents the usage information of one product on one crop in a specific region and year. The source data includes the following columns:

- **Active group (S)**
- **Time of use: Autumn/Spring (S)**: The time of year that the product is applied. This value is either Autumn, Spring, or Unknown.
- **Crop (S)**: The crop name.
- **Crop group (S)**: An aggregated crop group (e.g., cereals, tree fruits, or vegetables).
- **Product (S)**: The product's commercial name. This can also include other treatment types such as mechanical treatment, ploughing up, no treatment, or weather damage.
- **Product type segmentation (S)**: The general type of the product (e.g., Herbicide, Insecticide, Fungicide, or Aracicide).
- **Land (S)**: The federal state that this row provides information for.
- **District (S)**: One of 36 unique districts.
- **Crop year (S)**: A year between 1995 and 2020. 1995 data is incomplete.
- **Special - Region => Germany**: One of 56 unique districts
- **Avg. application rate (l or kg/ha)**: The average application rate of this product across all growers who reported using it.
- **Cultivated area sum 1000 ha (TCA)**: The total cultivated area of a crop in a region in a year. In units of 1000 ha.
- **SDA area 1000 ha (SDA)**: The total applied area of this product on a crop in a region in a year. It is possible for this value to be greater than the total cultivated area due to multiple applications of a product. In units of 1000 ha.
- **Tonnage (t)**: The application rate in l/ha or kg/ha multiplied by the total applied area (SDA area).

The crop names in the survey data were not the same as crop names in the spatial data, therefore, a mapping was implemented. Each survey crop name was mapped to a crop type from the national scale raster crop map of Germany.

[Survey to crop map codes mapping](../static/Survey-to-crop-map-codes.csv){:download="Survey-to-crop-map-codes.csv"}

## Calendar creation

To create the PPM Calendars for this scenario, the source survey data was joined with the survey to crop codes mapping file (linked above) to provide a crop map LULC code for each survey entry.

To calculate application probabilities, the following process was repeated for each year of the survey data:

1. Filter the survey data to one of the three possible values for time of use: Autumn, Spring, or Unknown. Steps 2-6 are repeated for each time of use.
2. Get all unique crop map LULC values that are present in the filtered survey data from step 1. Filter the survey data to only include records with crop map LULC codes equal to the first unique LULC code. Steps 3-6 are repeated for each crop map LULC value.
3. Calculate the total cultivated area for the crop map LULC code. This is calculated by summing the unique "Cultivated area sum 1000 ha (TCA)" values in the filtered data.
4. For each unique survey crop in the filtered data:
    1. Filter the survey data from step 2 to only include records with the unique survey crop type.
    2. Calculate the total cultivated area of that crop. Divide the survey crop's total cultivated area by the crop map LULC's total cultivated area to get the probability that a given field is that crop type. This calculation is necessary because the spatial data only contains information as detailed as the crop map LULC type, and the survey crop types are more detailed.
    3. Check if there are actually any applications to this survey crop in the filtered survey data. It is possible for the crop map LULC code to exist in the filtered survey data, but not each individial crop. If there are applications, continue to step 5.
5. For each product application in the survey data, compare the "SDA area 1000 ha (SDA)", or the total applied area of this product with the filtered data from step 4. If the SDA area is greater than the crop's total cultivated area, there must be at least one application of this product to every field. Subtract the total cultivated area value from the applied area value and compare them again. Stop once the applied area is less than or equal to the total cultivated area value. Note these applications in a separate PPM Calendar which applies this product to all fields of the current crop map LULC code/survey crop.
6. Add all applied area values of the filtered data. The chance of any one product being chosen equals the applied area of that product divided by the total applied area of all products from step 4.

A PPM Calendar for this scenario follows this structure (some elements omitted for space):

```xml
<TemporalValidity>
    dd-mm-yyyy to dd-mm-yyyy
</TemporalValidity>
<TargetCrops type="list[int]" scales="global">
    LULC code(int)
</TargetCrops>
<Indications type="xCropProtection.ChoiceDistribution" scales="time/year, space/base_geometry">
    <!-- Crop 1 -->
    <Indication probability="0.9">
        <Indication type="xCropProtection.ChoiceDistribution" scales="time/year, space/base_geometry">
        <ApplicationSequence probability="0.004579">
            ...
        </ApplicationSequence>
        <ApplicationSequence probability="0.106977">
            ...
        </ApplicationSequence>
        <ApplicationSequence probability="0.070475">
            ...
        </ApplicationSequence>
        ...
        </Indication>
    </Indication>
    <!-- Crop 2 -->
    <Indication probability="0.07">
        <Indication type="xCropProtection.ChoiceDistribution" scales="time/year, space/base_geometry">
        <ApplicationSequence probability="0.122716">
            ...
        </ApplicationSequence>
        <ApplicationSequence probability="0.219861">
            ...
        </ApplicationSequence>
        ...
        </Indication>
    </Indication>
    <!-- Crop 3 -->
    <Indication probability="0.03">
        <Indication type="xCropProtection.ChoiceDistribution" scales="time/year, space/base_geometry">
        <ApplicationSequence probability="0.028835">
            ...
        </ApplicationSequence>
        <ApplicationSequence probability="0.133795">
            ...
        </ApplicationSequence>
        ...
        </Indication>
    </Indication>
</Indications>
```

Example going from source table to final calendar:

## Results
