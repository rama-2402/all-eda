### Percentage and Sum of Missing values in each Columns
* creating a total missing column showing the number of missing values
* creating a perc_missing column to show the Percentage

 ```python
missing_data = pd.DataFrame({'total_missing': data.isnull().sum(), 'perc_missing': (data.isnull().sum()/data.shape[0])*100})
 ```

### Changing the datatype to datetime
* to_datetime -> converts the column values to datetime format
* erroes = 'coerce' -> will replace the invalid entires with NaN values so it is easier for future reference
```python
data.date_of_game = pd.to_datetime(data.date_of_game, errors='coerce')
```

### Trick to Changing the categorical data to numerical format
* get all the unique values from the categorical data
* create a range of numbers for the number of data present
* use replace to replace the values 
```python
l_unique = data['game_season'].unique() # fteching out the unique values from game_season
v_unique = np.arange(len(l_unique)) # obtaining values in the range of the length of I_unique
data['game_season'].replace(to_replace=l_unique, value=v_unique, inplace=True) # replacing categorical data with numerical values
```

### Replacing NaN values
* replacing with mean value
```python
data['power_of_shot'].fillna(value=data['power_of_shot'].mean(), inplace=True)
```
* replacing with mode value
```python
mode_com  = data.type_of_combined_shot.value_counts().keys()[0]
data.type_of_combined_shot.fillna(value=mode_com, inplace=True)
```
* replacing with median value
```python
data.remaining_sec.fillna(value=data.remaining_sec.median(), inplace=True)
```
* replacing with a range of values like a serial numbers 
```python
data.shot_id_number = pd.Series(np.arange(1,data.shot_id_number.shape[0]+1))
```
* replacing with a constant value 
```python
data['location_x'].fillna(value=0, inplace=True)
data['location_y'].fillna(value=0, inplace=True)
```
* Forward Flling
```python
col = ['home/away','lat/lng', 'team_name','match_id','match_event_id', 'team_id', 'remaining_min', 'knockout_match',  'game_season' ]
data.loc[:,col] = data.loc[:,col].ffill()
```
