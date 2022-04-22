# Predicting Waterpoint Functionality in Tanzania

![img](images/lake_victoria.jpg)

(Lake Victoria in Tanzania - image courtesy of [thepinkbackpack.com](https://www.thepinkbackpack.com/).)

## Overview

About 4 million of Tanzania's 59 million people lack access to potable (drinking) water; an even greater proportion of the Tanzanian population (nearly half) lack access to what water.org calls "[improved sanitation](https://water.org/our-impact/where-we-work/tanzania/)".

While the majority of Tanzanians *do* have access to clean water, a quick look at the functionality status of about 60,000 waterpoints (wells, pumps, etc.) indicates that nearly **half** of those waterpoints either need repair to function consistently.

![img](images/target_val_counts.jpg)

## Problem

The purpose of this project is to **predict the functionality of a waterpoint** given a certain set of attributes about the waterpoint.

## Data

Data for this project comes from an ongoing competition hosted by DrivenData, [*Pump it Up: Data Mining the Water Table*](https://www.drivendata.org/competitions/7/pump-it-up-data-mining-the-water-table/), which uses data from **Taarifa** and the **Tanzanian Ministry of Water**. Descriptions of each column in the dataset can be found at [this link](data_dict_basic.txt) within this repository.

## Methods

**pandas** was used for data wrangling and modification; **scikit-learn**'s various libraries and classes were used in preprocessing the data & formulating models.

Thorough exploratory analysis revealed that a number of the dataset's forty columns (features) contained information that was redundant with other columns, not informative to the modeling process, or otherwise superfluous.

Following the consolidation of the data, pipelines were created to minimize data leakage, and an iterative modeling process followed. The final model incorporated scikit-learn's `RandomForestClassifier` algorithm and the XGBoost `XGBClassifier` algorithm.

## Results

### Training Data

- Accuracy score: **0.85**
- F1 scores:
    - `functional` - **0.88**
    - `non functional` - **0.85**
    - `functional needs repair` - **0.51**


### Testing on Unseen Data

- Accuracy score: **0.79**
- F1 scores:
    - `functional` - **0.83**
    - `non functional` - **0.78**
    - `functional needs repair` - **0.33**
- Precision score for `non functional` predictions: **0.84**


## Conclusion

Examining the model's performance - more specifically, its accuracy, F1, and, for the `non functional` status group, precision scores - on unseen (testing) data, we can conclude the following:

- **In general,** our model *accurately predicts* whether a given well will be functional, not functional, or functional (but in need of repair) about **79% of the time**. In other words, we make a correct prediction **four out of five times**.
- The precision score for predictions on **non-functional** wells - **0.84** - indicates the rate of **true positives**.

### Next Steps

- **Improve data gathering practices:**
    - The dataset contains many columns where unknown values were inputted as zeroes - see `construction_year`, `longitude` / `latitude`, `amount_tsh`, among others. This is **important data!**
    - More accurate data collection will reduce errors in the training process, which will, in turn, produce better results on unseen data, and better predictions on which waterpoints need attention.
- **Granular investigation into individual features:**
    - i.e. Which aspects of a waterpoint are most relevant and useful to the predictive process?
    - Time and resource limitations prevented me from conducting more comprehensive column analysis; calculating feature importance with `sklearn` will almost inadvertently yield better results than my manual, intuitive process.
- **Optimize construction of new waterpoints:**
    - Inquiry into what attributes of a waterpoint best predict its functionality will **also** yield invaluable information about **what to prioritize** when constructing new wells.
    - While this project covers only the need to attend to **existing waterpoints**, I recognize that a time will inevitably come when new builds are necessary. Analyzing various aspects of a waterpoint in conjunction with time-based features like `construction_year` and `date_recorded` will provide insight on how to construct waterpoints that are both efficient and sustainable. 
    
    
## Repository Structure
```
├── Jupyter_Notebooks
│       ├── Exploratory_Analysis_and_Cleaning.ipynb
│       └── Modeling_Scratchwork.ipynb
│
├── data (note: only the .csv files marked with an
│   asterisk * are necessary to run notebook)
│       ├── training_set_values.csv*
│       ├── training_set_labels.csv*
│       ├── test_set_values.csv
│       ├── test_set_labels.csv
│       └── data_dict_basic.txt
│
├── images
│       ├── lake_victoria.jpg
│       ├── pangani_river.jpg
│       └── target_val_counts.jpg
│
│
├── Predicting_Waterpoint_Functionality.ipynb
├── presentation.pdf
├── LICENSE
└── README.md
```
### Further reading and citations

Full analysis available in [Jupyter notebook](Predicting_Waterpoint_Functionality.ipynb).

Non-technical presentation slides [available in .pdf format](presentation.pdf).
