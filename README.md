# EDA-Question-Anwser
wings-MFAO-Exploratory data analysis's 

import pandas as pd  
import numpy as np  


### Read the data (this will not be graded)

c_data = pd.read_csv('data.csv')  
print(c_data)

# What is the standard deviation of maximum windspeed across all the days
ws_std1 = round(c_data.std(axis=0,skipna=True)['Maximum windspeed (mph)'],2)  
print(ws_std1)  
ws_std = 13.06  

​

# What is the difference between 50th percentile and 75th percentile of average temperature
p1 = c_data['Average temperature (°F)']   
pran =  round(np.percentile(p1,50,interpolation='lower') - np.percentile(p1,75,interpolation='lower'),2)  
print(pran)  
p_range = 12.20  

# What is the pearson correlation between average dew point and average temperature
c1 = c_data['Average dewpoint (°F)']    
c2 = c_data['Average temperature (°F)']  
cor =round(np.corrcoef(c1,c2)[0,1],2)  
print(cor)  
corr = 0.76  

# Out of all the available records which month has the lowest average humidity.
# - Assign your answer as month index, for example if its July index is 7
​
h2=c_data[['Day','Average humidity (%)']]  
min1 = h2.min()  
min1['Day'] = pd.to_datetime(min1['Day'],format='%d/%m/%Y')  
dew =min1['Day'].month  
print(dew)  

dew_month = 1  

​
​
​
# Which month has the highest median for maximum_gust_speed out of all the available records. Also find the repective value

d2 = c_data[['Day','Maximum gust speed (mph)']]  
d2['Day'] = pd.to_datetime(d2['Day'],format='%d/%m/%Y')  
g1 = d2.groupby(by=d2.Day.dt.month)  
g2 = g1.median()  
g2.rename(columns={'Maximum gust speed (mph)':'gust'},inplace=True)  
maxx = g2.max()  

dd1 = g2[g2.gust == 34.5]  

s3 = format(round(maxx['gust'],2),'.2f')  
s4 =  int(dd1.index.values)  
print(s3)  
print(s4)  
max_gust_value = 34.50  
max_gust_month = 2  



# Determine the average temperature between the months of March 2010 to May 2012 (including both the months)
t1 = c_data[['Day','Average temperature (°F)']]  
t1.rename(columns={'Average temperature (°F)':'temp'},inplace=True)  
t1['Day']=pd.to_datetime(t1['Day'],format='%d/%m/%Y')  
ds1 = t1.sort_values(by="Day")  
start_date = '2010-03-01'  
end_date = '2012-05-31'  
mask = (ds1['Day']>=start_date)&(ds1['Day']<=end_date)  
ds2 = ds1.loc[mask]  
s5 = round(ds2['temp'].mean(),2)  
print(s5)  
avg_temp = 45.89  
​

# Find the range of averange temperature on Dec 2010
# temp_range
start_date1 = '2010-12-01'  
end_date1 = '2010-12-31'  
mask1 = (ds1['Day']>=start_date1)&(ds1['Day']<=end_date1)  
ds3 = ds1.loc[mask1]  
ran = ds3['temp'].max() - ds3['temp'].min()  
s6 = format(ran,'.2f')  
print(s6)  
temp_range = 44.80  


#
# Out of all available records which day has the highest difference between maximum_pressure and minimum_pressure
# - assign the date in string format as 'yyyy-mm-dd'. Make sure you enclose it with single quote


p3 = c_data[['Day','Minimum pressure ','Maximum pressure ']]  
p3.rename(columns={'Minimum pressure ':'mnp','Maximum pressure ':'mxp'},inplace=True)  
p3['Day']=pd.to_datetime(p3['Day'],format='%d/%m/%Y')  
p3['diff'] = round(p3['mxp'] - p3['mnp'],2)  

max2 = p3.sort_values(by='diff')[::-1].iloc[0]  


dat = max2.Day.date()  
print(dat)  

max_p_range_day = '2018-03-23'  


# How many days falls under median (i.e equal to median value) of barrometer reading.
m1 = c_data[['Day','Average barometer (in)']]  
m1.rename(columns={'Average barometer (in)':'ab',},inplace=True)  
m1['Day']=pd.to_datetime(m1['Day'],format='%d/%m/%Y')  
med1 = m1.median().ab  
x1 =  m1[m1.ab==med1]  


s7 = x1.shape[0]  
print(s7)  

median_b_days = 534  
​
​
# ​Out of all the available records how many days are within one standard deviation of average temperaturem

p5 = c_data[['Day','Average temperature (°F)']]  
stdv  = round(p5.std(axis=0,skipna=True)['Average temperature (°F)'],2)  
p5.rename(columns={'Average temperature (°F)':'tb',},inplace=True)  
mean2 = round(p5.mean(),2).tb  
​
nm = p5[abs(p5.tb - mean2)<=stdv ]  
​
s8 = nm.shape[0]  
print(s8)  
​ 
num_days_std = 2092  
​
