# DublinBikes Station Occupancy Analysis

This project analyses **DublinBikes** station occupancy patterns using the Dublin City Council (DCC) DublinBikes dataset from Kaggle (2019–2023). The goal is to understand how station usage varies over time and to group stations into meaningful clusters based on their occupancy behaviour.

Dataset on Kaggle: https://www.kaggle.com/datasets/mexwell/dublinbikes-dcc-dataset  

---

## Project overview

- Use historical DublinBikes data (hourly availability) for 2019–2023 to study station occupancy.  
- Perform exploratory data analysis (EDA) and visualization to understand temporal and spatial patterns.  
- Engineer an **occupancy rate** feature from available stands and total stands.  
- Apply **K-Means clustering** to segment stations and validate clusters using inertia and silhouette scores.

---

## Data

- Source: *Dublinbikes DCC Dataset* from Kaggle. The dataset provides hourly bike availability at DublinBikes stations, with monthly files for 2022–2023 and quarterly files for 2019–2021. [web:81][web:82]  
- Files used:
  - All station data files from 2019–2023.
  - The address/metadata file was excluded from modelling (used only for reference if needed).

Key variables:
- `TIME` / timestamp  
- `STATION ID`  
- `AVAILABLE BIKES`  
- `AVAILABLE STANDS`  
- `TOTAL STANDS`  

---

## Methodology

### 1. Data cleaning and preprocessing

- Ignored the metadata‑only file and loaded all remaining CSV files for 2019–2023.  
- Removed duplicate rows to avoid bias from repeated measurements.  
- Treated the data as a time series and used **forward fill** to impute missing values within each station’s time series.  
- Created a consolidated dataset with a clean datetime index and standardised column names.

### 2. Feature engineering

- Engineered an **occupancy rate** feature for each station and timestamp:

  \[
  \text{occupancy\_rate} = \frac{\text{total\_stands} - \text{available\_stands}}{\text{total\_stands}}
  \]

  This measures the proportion of stands currently occupied and normalises usage across stations with different capacities. [web:85]

- Used **quartile-based segmentation** (e.g. low/medium/high occupancy based on quartiles) as a base-level segmentation to interpret station behaviour.

### 3. Exploratory data analysis (EDA)

- Created time‑series plots and aggregated summaries to examine:
  - Daily and weekly occupancy trends.  
  - Differences between weekdays and weekends.  
  - Seasonal changes over 2019–2023.  

- Used scatter plots and other visualisations to explore relationships between occupancy rate, station capacity, and time of day.

### 4. Clustering

- Scaled numeric features (e.g. occupancy statistics, capacity metrics, temporal aggregates) before clustering.  
- Applied **K-Means clustering** to group stations based on their occupancy patterns over time.  
- Used the **inertia (elbow) method** to select a candidate range for the number of clusters.  
- Computed **silhouette scores** to validate and refine the choice of optimal cluster count.  
- Visualised clusters with scatter plots to interpret groups (e.g. consistently full vs. underused stations).

---

## How to run

1. **Clone the repository** 
2. **Create and activate a virtual environment** (optional but recommended)
3. **Install dependencies**

4. **Download data**

- Download the DublinBikes DCC dataset from Kaggle:  
  https://www.kaggle.com/datasets/mexwell/dublinbikes-dcc-dataset  
- Place the CSV files into `data/raw/`.

5. **Run notebooks**

- Start Jupyter:

  ```
  jupyter notebook
  ```

- Open and run:
  - `notebooks/DublinBikesOccupancy.ipynb`  
---

## Results and findings

- The clustering approach identifies groups of stations with distinct occupancy profiles (e.g. consistently busy vs. underutilised). [web:83][web:97]  
- Quartile‑based segmentation and occupancy rate help prioritise stations that are frequently full/empty, which can inform rebalancing strategies or infrastructure planning. [web:83][web:85]

---

## Future work

- Incorporate external data such as weather and events to explain occupancy patterns. [web:83]  
- Experiment with other clustering techniques (DBSCAN, hierarchical clustering) and time‑series models for forecasting station occupancy. [web:91]  
- Build an interactive dashboard to explore station‑level occupancy and cluster assignments.

---

## Acknowledgements

- **Data**: DublinBikes DCC dataset on Kaggle. [web:81][web:82]  
- **Context**: DublinBikes scheme operated by Dublin City Council and Smart Dublin open data initiatives. [web:84][web:87][web:90]




