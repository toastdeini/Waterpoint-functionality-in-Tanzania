# Predicting Waterpoint Functionality in Tanzania

![img](images/lake_victoria.jpg)

(Lake Victoria in Tanzania - image courtesy of [thepinkbackpack.com](https://www.thepinkbackpack.com/).)

## Overview

## Problem

About 4 million of Tanzania's 59 million people lack access to potable (drinking) water; an even greater proportion of the Tanzanian population (nearly half) lack access to what water.org calls "[improved sanitation](https://water.org/our-impact/where-we-work/tanzania/)".

## Data

Data for this project comes from an ongoing competition hosted by DrivenData, [*Pump it Up: Data Mining the Water Table*](https://www.drivendata.org/competitions/7/pump-it-up-data-mining-the-water-table/), which uses data from **Taarifa** and the **Tanzanian Ministry of Water**. Descriptions of each column in the dataset can be found at [this link](data_dict_basic.txt) within this repository.

## Methods

pandas was used for data wrangling and modification; scikit-learn's various libraries and classes were used in preprocessing the data & formulating models.

Thorough exploratory analysis revealed that a number of the dataset's forty columns (features) contained information that was redundant with other columns, not informative to the modeling process, or otherwise superfluous.

## Results

### Accuracy on Unseen Data

## Conclusion

### Next Steps

## Repository Structure
```
├── Jupyter_Notebooks
│      ├── Exploratory_Analysis_and_Cleaning.ipynb
│      ├── Modeling_Scratchwork.ipynb
│      └── .ipynb
│
├── data
│      ├── .csv
│      ├── .csv
│      ├── .csv
│      ├── .csv
│      └── data_dict_basic.txt
├── images
│      ├── lake_victoria.jpg
│      └── .jpg
│
├── Predicting_Waterpoint_Functionality.ipynb
├── presentation.pdf
├── LICENSE
└── README.md
```
### Further reading and citations

Full analysis available in [Jupyter notebook](Predicting_Waterpoint_Functionality.ipynb).

Non-technical presentation slides [available in .pdf format](presentation.pdf).
