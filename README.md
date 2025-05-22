# ✈️ Flight Price Dataset - Exploratory Data Analysis (EDA)

This project involves cleaning, preprocessing, and performing Exploratory Data Analysis (EDA) on a flight price dataset to understand key patterns and features that influence flight pricing.

## 📁 Dataset Source

- **Columns**: `Airline`, `Source`, `Destination`, `Route`, `Dep_Time`, `Arrival_Time`, `Duration`, `Total_Stops`, `Additional_Info`, `Price`
- **Rows**: Includes thousands of domestic flight records from India

## 🛠️ Tools Used

- **Language**: Python 🐍
- **Libraries**:
  - `pandas`, `numpy` – Data manipulation
  - `matplotlib.pyplot`, `seaborn` – Data visualization
  - `sklearn.preprocessing` – OneHotEncoding for categorical features

## 🔍 Key Steps in the Notebook

### 1. Data Cleaning & Preprocessing
- Extracted useful date/time components:
  - `Dep_Time` → `Departure_hour`, `Departure_min`
  - `Arrival_Time` → `Arrival_hour`, `Arrival_min`
  - `Date_of_Journey` → `Day`, `Month`, `Year`
- Converted `Duration` into `Duration_hour` and `Duration_min`
- Handled missing values in `Total_Stops` by replacing with mode
- Mapped `Total_Stops` to numeric values:  
  `'non-stop'` → 0, `'1 stop'` → 1, etc.

### 2. Encoding Categorical Variables
- Applied `OneHotEncoder` to:
  - `Airline`
  - `Source`
  - `Destination`
  - `Additional_Info`

### 3. Final Dataset Construction
- Dropped original categorical columns after encoding
- Merged encoded dataframe with numeric features

## 📊 Possible Analysis (To Explore)
- Which airlines charge the most?
- How does number of stops affect the price?
- Correlation between duration and price
- Price comparison across different cities and routes

## 📌 Sample Preprocessing Code

```python
from sklearn.preprocessing import OneHotEncoder
encoder = OneHotEncoder()
encoded_df = pd.DataFrame(
    encoder.fit_transform(df[['Airline', 'Source', 'Destination', 'Additional_Info']]).toarray(),
    columns=encoder.get_feature_names_out()
)
final_df = pd.concat([df.reset_index(drop=True), encoded_df.reset_index(drop=True)], axis=1)
