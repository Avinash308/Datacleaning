# Datacleaning
Removing columns from dataset, interpolate, replacing columns

#cleaning the data removing unneccessary data
import numpy as np
import pandas as pd
df = pd.DataFrame({'From_To': ['LoNDon_paris', 'MAdrid_miLAN', 'londON_StockhOlm',
'Budapest_PaRis', 'Brussels_londOn'],
'FlightNumber': [10045, np.nan, 10065, np.nan, 10085],
'RecentDelays': [[23, 47], [], [24, 43, 87], [13], [67, 32]],
'Airline': ['KLM(!)', '<Air France> (12)', '(British Airways. )',
'12. Air France', '"Swiss Air"']})
print(df)
  
df['FlightNumber']=df['FlightNumber'].interpolate().astype(int)
df

#from_to would be better if we have a 2 seperate columns, split them from "_"
#the underscore to give a new temporary dataframe with correct values
new=df['From_To'].str.split('_',n=1,expand=True)
new.columns=['From','To']
new

new['From']=new['From'].str.title()
new['From']
new['To']=new['To'].str.title()
new['To']
new.columns=['From','To']
new

#removing from_to column in data set and replace it with new
df.drop(columns=['From_To'],inplace=True)
df['From']=new['From']
df['To']=new['To']
df
