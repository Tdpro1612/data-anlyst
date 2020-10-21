# data-anlyst
first exam data(i work with 3 persons in team 5)
we get data from kaggle https://www.kaggle.com/START-UMD/gtd?select=globalterrorismdb_0718dist.csv
we chose year from 1997 -> future
we used google.colab
### What is my data about?
Information on 180,000 terrorist attacks
Around the world from 1970 through 2017. 
- It includes systematic data on domestic as well as international terrorist. 
- There are no plots, conspiracies and unsuccessful attacks. 

### Target Audience: 
- Business Invester who want to find a safe place to invest their money without the fear about terrorist attacks.

### Data details
- Incidents location
- Date and time the incident happened
- Incident information
  - Attack type
  - Attack target
  - Group of Perpetrator 
  - Incident Motive

### Evaluation metrics
Based on 2 metrics
- Casualties: a combination of killed and wounded victims
- Damaged Property value: the estimation of damaged property by USD.

### Hypothesis:
- Which is the most countries was aim by terrorism?
- Where is the most dangerous place to to stay in terms of terrorism?
- Where is the place we can get least damage from a terrorist attack?

### Exploration ideas:
- The rise of all terrorism around the world
- Top 10 nationality of target victim and a casuality 
- Top 10 Countries that most affected by terrorism
- Top 10 terrorism Activities by Type of attack and target
- What is the common motive of all kind terrorism in the world
- Top 10 Terrorist Groups with Highest Terror Attacks
- Growth of damaged property value and casuality of US
- Which US target that was attacked mostly?

# Import Library
``` 
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

import warnings
warnings.filterwarnings('ignore')

sns.set_style("whitegrid")
```
### clean and clear data
- read data 
``` 
terr = pd.read_csv('path forder you upload it/terrorism.csv',encoding='latin-1')
```
- Show a summary of the data
```
terr.info()
- Show a sample
terr.sample(10)
```
- check null file and duplicate file then we drop it

```
terr['eventid'].nunique() == terr.shape[0]
```
- Rename used columns
```
terr.rename(columns={'iyear':'Year','imonth':'Month','propvalue':'DamagedPropertyValue',
                       'iday':'Day','country_txt':'Country','latitude':'Latitude','longitude':'Longitude',
                       'region_txt':'Region','attacktype1_txt':'AttackType','city':'City',
                       'target1':'Target','nkill':'Killed','nkillus':'KilledUS',
                       'nwound':'Wounded','nwoundus':'WoundedUS','eventid':'ID',
                       'gname':'Group','targtype1_txt':'TargetType','natlty1_txt':'TargetNationality',
                       'weaptype1_txt':'WeaponType','motive':'Motive'},inplace=True)
 ```                    
- Get columns
```
terr=terr[['Year','Month','Day','Country',
           'Region','City','WoundedUS',
           'KilledUS','AttackType','ID','Latitude','Longitude',
           'Killed','Wounded','Target','DamagedPropertyValue',
           'Group','TargetType','WeaponType',
           'Motive','TargetNationality']]
 ```
- Drop data before 1997
```
terr.drop(labels=terr[terr['Year'] < 1997].index, axis=0, inplace=True)          
```
- Manipulate **data**
- Check for missing data
```
terr.isnull().sum()
```
- Fill NaN to city, Target, Summary, Motive
```
terr['City'].fillna("Unknown", inplace=True)
terr['Target'].fillna("Unknown", inplace=True)
terr['Region'] = terr['Region'].astype('category')
terr['Motive'].fillna("Unknown", inplace=True)
```
- Fill NaN to 0 for Killed and Wounded
```
terr['Killed'].fillna(0, inplace=True)
terr['Killed'] = terr['Killed'].astype(int) 
terr['Wounded'].fillna(0, inplace=True)
terr['Wounded'] = terr['Wounded'].astype(int) 
terr['KilledUS'].fillna(0, inplace=True)
terr['KilledUS'] = terr['KilledUS'].astype(int)
terr['WoundedUS'].fillna(0, inplace=True)
terr['WoundedUS'] = terr['WoundedUS'].astype(int)
```
- Fill NaN to Nationality False
```
terr['TargetNationality'].fillna("No data", inplace=True)
terr['TargetNationality'] = terr['TargetNationality'].astype('category')
```
- File NaN to Property Damage
```
terr['DamagedPropertyValue'].fillna(0, inplace=True)
terr['DamagedPropertyValue'] = terr['DamagedPropertyValue'].apply(lambda x: 0 if x < 0 else x)
```
- Change data type
```
terr['Country'] = terr['Country'].astype('category')
terr['City'] = terr['Country'].astype('category')
terr['Group'] = terr['Group'].astype('category')
terr['WeaponType'] = terr['WeaponType'].astype('category')
```
etc....

## we explore it
![The rise of all terrorism around the world](https://user-images.githubusercontent.com/61773507/96667985-5950a400-1384-11eb-86c7-5b42bd001455.png)

![Top 10 nationality of target victim and a casuality](https://user-images.githubusercontent.com/61773507/96668285-0aefd500-1385-11eb-9ef9-69578b353a5a.png)

