# Predicting Waterpoint Functionality in Tanzania

![img](images/lake_victoria.jpg)

(Lake Victoria in Tanzania - image courtesy of [thepinkbackpack.com](https://www.thepinkbackpack.com/).)

## Overview

About 4 million of Tanzania's 59 million people lack access to potable (drinking) water; an even greater proportion of the Tanzanian population (nearly half) lack access to what water.org calls "[improved sanitation](https://water.org/our-impact/where-we-work/tanzania/)".

While the majority of Tanzanians *do* have access to clean water, a quick look at the functionality status of about 60,000 waterpoints (wells, pumps, etc.) indicates that nearly **half** of those waterpoints either need repair to function without interruption ***or*** don't function at all.

![img](images/target_val_counts.jpg)

## Problem

The Tanzanian Ministries of Water and Health have received a grant from the World Health Organization (WHO) to be used in refurbushing the country's existing water sources. However, the grant cannot sufficiently finance a complete overhaul of the water supply system - time and resources are limited, and the field directors responsible for selecting **where** to position their technicians will need to make judicious, informed decisions about which waterpoints are worth visiting.

Of course, the Ministries and their staff/technicians will *not* always know if a waterpoint is functional prior to actually visiting the waterpoint - this is where the machine learning modeling comes in handy.

Given a set of descriptive attributes about the waterpoint, but not knowing its true functionality status, I was able to construct a model that accurately predicts a waterpoint's functionality status with 79% accuracy.

## Data

Data for this project comes from an ongoing competition hosted by DrivenData, [*Pump it Up: Data Mining the Water Table*](https://www.drivendata.org/competitions/7/pump-it-up-data-mining-the-water-table/), which uses data from **Taarifa** and the **Tanzanian Ministry of Water**. Descriptions of each column in the dataset can be found at [this link](data_dict_basic.txt) within this repository.

The full dataset has forty columns (potential features), each containing information about various attributes of a waterpoint: its latitude and longitude, the year of its construction, and the quality of water a pump provides, and a few dozen others. Not all of these features were ultimately used in modeling; the [exploratory data analysis notebook](Jupyter_Notebooks/Exploratory_Analysis_and_Cleaning) has more verbose insight into the feature selection process.

## Methods

**pandas** was used for data wrangling and modification; **scikit-learn**'s various libraries and classes were used in preprocessing the data & formulating models.

Thorough exploratory analysis revealed that a number of the dataset's forty columns (features) contained information that was redundant with other columns, not informative to the modeling process, or otherwise superfluous.

Following the consolidation of the data, pipelines were created to minimize data leakage, and an iterative modeling process followed. The final model incorporated scikit-learn's `RandomForestClassifier` algorithm and the XGBoost `XGBClassifier` algorithm. See the [modeling notebook](Jupyter_Notebooks/Modeling_Scratchwork) for further information - be aware that some of the models may take a while to run, depending on the power of your machine.

## Results

### On training data

- Accuracy score: **0.85**
- F1 scores:
    - `functional` - **0.88**
    - `non functional` - **0.85**
    - `functional needs repair` - **0.51**

### Testing on unseen data

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

By targeting waterpoints whose features and attributes are likely to correspond with non-functionality, we can emphasize refurbishing water supplies in the hardest hit areas without diverting unnecessary resources to waterpoints that are fully operational.

### Next Steps

- **Improve data gathering practices:**
    - The dataset contains many columns where unknown values were inputted as zeroes - see `construction_year`, `longitude` / `latitude`, `amount_tsh`, among others. This is **important data!**
    - More accurate data collection will reduce errors in the training process, which will, in turn, produce better results on unseen data, and better predictions on which waterpoints need attention.
    - This data **can also be actively collected and updated** in the refurbishing process.
- **Granular investigation into individual features:**
    - i.e. Which aspects of a waterpoint are most relevant and useful to the predictive process?
    - Time and resource limitations prevented me from conducting more comprehensive column analysis; calculating feature importance with `sklearn` will almost inadvertently yield better results than my manual, intuitive process.
    - Some features that were used in this predictive model might be **unavailable** in future analysis - for instance, while I included the quality of water that a waterpoint provides (`quality_group`) as a feature in my final model, it is a more fluid and unpredictable metric than, say, latitude or longitude.
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
