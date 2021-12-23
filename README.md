# set up import statements for all of the packages
import csv
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
% matplotlib inline
df = pd.read_csv('Database_No_show_appointments/noshowappointments-kagglev2-may-2016.csv')
df.head()

# Datacleaning Section
# ScheduledDay convert to Datetime
df['ScheduledDay'] = pd.to_datetime(df['ScheduledDay'], format="%Y-%m-%dT%H:%M:%SZ")
# timedata is not for use
df['ScheduledDay'] = df['ScheduledDay'].dt.floor("D")
# AppointmentDay convert to Datetime
df['AppointmentDay'] = pd.to_datetime(df['AppointmentDay'], format="%Y-%m-%d")
# Days means how manydays away from ScheduledDay to AppointmentDay
df['Days']=df['AppointmentDay']-df['ScheduledDay']
# rename column
df.rename(columns={'No-show':'No_show'},inplace = True)

df.info()
df.head()
df.hist(figsize= (10,8));

# Exploratory Data Analysis Section
# Filter No_show
df_noshow_y=df.query('No_show == "Yes"')
df_noshow_y.head()
df_noshow_n=df.query('No_show == "No"')
df_noshow_n.head()

# Histgram
df['Days'].hist(by=df['No_show'])
plt.show()
