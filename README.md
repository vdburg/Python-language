# Python-language
Tips to manipulate objects in Python

#Get current working directory
import os
os.getcwd()
#Change Working directory
os.chdir('D:\Varios\Python')
#list files in working directory
%ls   

#### Basics
#Create array
b =np.array([
       [ 0,  1,  2,  3],
       [10, 11, 12, 13],
       [20, 21, 22, 23],
       [30, 31, 32, 33],
       [40, 41, 42, 43]]
       )
#If I use sum it sums all elements      
b.sum()
#If I want to sum only the elements of the first column
b[:,1].sum() 

#Split function will separate elements with ',' replacing the current defined separator
a= "Hola Campeones del mundo"
a.split(' ')

#### Using for loop
#sum elements of a list os elements and print it
puntos = ((0,1), (1,2), (1,3))
for (x,y) in puntos:
    print( x + y )
#Puts previous output into a list    
z=[]    
for (x,y) in puntos:
    z.append(x+y)
#Use a comprehension to achieve the same
u=[x+y for (x,y) in puntos]



####Playing with tables like in SQL
#open a file with pandas and convert it into a dataframe
pledgers=pd.read_table(open('Pledgers.txt'))
#Object´s structure
type(pledgers)
#data projection using position
pledgers.iloc[1:5,0:4]
#data projection using names
pledgers.loc[1:5, ['ID','Campaign','Age']]
#Filtering in dataframe ('&' es un 'and' y '|' es un 'or')
pledgers[(pledgers.Age>35) | (pledgers.Gender=='M')]
#group by in dataframe (this will give the mean for all float columns)
pledgers[(pledgers.Age>35) | (pledgers.Gender=='M')].groupby(['Campaign']).mean()
#get mean and sum of specific column (you have to use agg and for mean you need to import numpy -I called numpy as np-)
pledgers.groupby(['Campaign']).LTV.agg([np.mean, np.sum])
#Get grouped mean of a column and convert into dataframe
pled1=pledgers.groupby(['Campaign']).Age.mean()
pled=pled1.add_suffix('_Count').reset_index()
pled

#Useful information http://pandas.pydata.org/pandas-docs/stable/groupby.html

doc=prueba_tweets() 
doc.head()
newdoc=doc['statuses']
new=newdoc[0]
doc=doc['statuses'][0].keys()
type(doc)

help(np.savetxt)

wanted_keys = ['coordinates','created_at','lang','place', 'text','id'] # The keys you want
twitter_data=dict((k, doc[k]) for k in wanted_keys if k in doc)

docent=doc['entities']
wanted_keys1 = ['hashtags','expanded_url','land','location','screen_name','text'] # The keys you want
twitter_data.update(dict((k, docent[k]) for k in wanted_keys1 if k in docent))

docurl=doc['entities']['urls'][0]
twitter_data.update(dict((k, docurl[k]) for k in wanted_keys1 if k in docurl))

docuer=doc['user']
twitter_data.update(dict((k, docuer[k]) for k in wanted_keys1 if k in docuer))
docret=doc['retweeted_status']
twitter_data.update(dict((k, docret[k]) for k in wanted_keys1 if k in docret))
