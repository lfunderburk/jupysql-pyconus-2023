# jupysql-pyconus-2023

Lighting talk: Catherin Devlin, Laura Funderburk

### Note about the data

This data was sourced from Kaggle via their API. For the purpose of the talk, the data is provided, but to give credit and enable openness and reproducibility, the following was done to obtain the data.

Install kaggle

```
pip install kaggle
```

Log in, generate and API key, then run

```
mkdir ~/.kaggle
mv kaggle.json ~/.kaggle/
chmod 600 ~/.kaggle/kaggle.json
```

The following data cleaning was done

```
import kaggle
import pandas as pd

kaggle.api.authenticate()
kaggle.api.dataset_download_files('papercool/organics-purchase-indicator', path='./', unzip=True)

# Perform data cleaning
df = pd.read_csv('organics.csv')
df = df.dropna()

# Rename columns: substitute spaces with underscores
df.columns = [c.replace(' ', '_') for c in df.columns]

# Convert Affluence_Grade, Age, Frequency_Percent to numeric
df['Affluence_Grade'] = pd.to_numeric(df['Affluence_Grade'], errors='coerce')
df['Age'] = pd.to_numeric(df['Age'], errors='coerce')
df['Frequency_Percent'] = pd.to_numeric(df['Frequency_Percent'], errors='coerce')

# Save the cleaned dataframe to local CSV file
df.to_csv('organics_cleaned.csv', index=False)

```