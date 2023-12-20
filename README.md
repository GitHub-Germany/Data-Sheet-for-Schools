# Data-Sheet-for-Schools

import pandas as pd
import matplotlib as mpl
import numpy as np

#upload Student Data
df_uni=pd.read_excel('generic uni data.xlsx',sheet_name='Student Data')

#print(df_can.head())
#print(df_can.tail())

# in pandas axis=0 represent rows (default), axis=1 represents columns
df_uni.drop(['Aid Type', 'ID', 'Pell Grant Amount', 'Postal Code', 'City'], axis=1, inplace=True)
#print(df_can.head())


#Filters for cali students
df_uni.set_index(['State'],inplace=True)
df_cali=df_uni.loc['California']


#Filters for female students
df_uni.set_index(['Gender'],inplace=True)
df_female=df_uni.loc['female']

#print(df_cali.head())
#print(df_female.head())

#------------------------------------------------------------------------------

''#Opening School Sheet
skool_sheet = pd.read_excel('generic uni data.xlsx',sheet_name='Schools')

#total sum
skool_sheet['Total']=skool_sheet.sum(axis=1, numeric_only=True)

#Sorted
#skool_sheet.sort_values(['Total'], ascending=False, axis=0, inplace=True)

skool_sheet.set_index('School', inplace=True)

#skool_sheet.columns = list(map(str, skool_sheet.columns))

#Defining a new variable and combining years 08-18
years_08_to_18=list(map(str, range(2008,2019)))

#Find Business and Management and plot a line chart
BusMan = skool_sheet.loc['Business and Management', years_08_to_18] 
BusMan.head()

#plotted info of just Bus and Man
BusMan.plot(kind='line')
plt.title('Business and Management')
plt.ylabel('Amount')
plt.xlabel('Years')
plt.show()

skool_sheet_5 = skool_sheet.head()

# Filter the dataframe for the specified years
skool_08_to_18_5 = skool_sheet_5[years_08_to_18].transpose()

#plotted info the scholarships compared
skool_08_to_18_5.plot(kind='line')
plt.title('Scholarship Amount')
plt.ylabel('Amount')
plt.xlabel('Years')
plt.show()

#--------------------------------------------------

#Opening Program Sheet
program_sheet = pd.read_excel('generic uni data.xlsx',sheet_name='Programs')
program_sheet['Total']=program_sheet.sum(axis=1, numeric_only=True)
program_sheet.sort_values(['Total'],ascending=False,axis=0,inplace=True)
program_sheet.set_index('Program', inplace=True)



#Top 5
program_sheet_5 = program_sheet.head()

years_08_to_18=list(map(str, range(2008,2019)))

# Filter the dataframe for the specified years
program_sheet_5 = program_sheet_5[years_08_to_18].transpose()


program_sheet_5.plot(kind='area',alpha= 0.45, figsize=(10, 8))
plt.title('Highest Amount of Scholarship 08-18')
plt.ylabel('Number of Scholars')
plt.xlabel('Year')
plt.show()

#Plotting hist


top3skool=program_sheet.loc[['Computer Science', 'Information Management','Business Administration'],years_08_to_18].transpose()

count,bin_edges=np.histogram(top3skool,5)


top3skool.plot(kind='hist',figsize=(8,5))
plt.title('scholarship amount distribution for Computer Science, Information Management, and Business Administration between 2008-2018')
plt.ylabel('Years')
plt.xlabel('Scholarships')
plt.show()
