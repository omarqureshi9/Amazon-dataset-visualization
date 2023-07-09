#Importing necessary libraries

import pandas as pd

import seaborn as sns

import matplotlib.pyplot as plt

import numpy as np

#Importing dataset

dataset=pd.read_csv("Amazon.csv")

#Styling graph grid as per my preference

sns.set_style("darkgrid")

#Coverting the date column to a format that pandas recognizes as date

dataset["Date"] = pd.to_datetime(dataset["Date"])

#Plotting time series graph of whole dataset of closing values

plt.figure(figsize=(12, 6))

plt.title("Closing value of Amazon shares")

plt.xlabel("Years")

plt.ylabel("Closing value")

plt.plot(dataset.Date, dataset.Close);


#Plotting time series graph of volumes

plt.figure(figsize=(12, 6))

plt.title("Amazon share volumes")

plt.xlabel("Years")

plt.ylabel("Volume")

plt.plot(dataset.Date, dataset.Volume, 'midnightblue');

#Plotting graph of intra-day high values of Amazon stock

plt.figure(figsize=(12, 6))

plt.title("Highest intra-day prices of Amazon stock")

plt.xlabel("Years")

plt.ylabel("Stock price")

plt.plot(dataset.Date, dataset.High, 'crimson');

#plotting volume against closing value

plt.figure(figsize=(12, 6))

plt.title("Volume against closing")

plt.xlabel("Volume")

plt.ylabel("Closing price")

plt.scatter(dataset.Volume, dataset.Close);

#Plotting time series of volume and closing value alongside volume-closing value scatter for better analysis

fig, axes = plt.subplots(3, 1, figsize=(10,10))

axes[0].plot(dataset.Date, dataset.Close, 'r')

axes[0].set_xlabel('Year')

axes[0].set_ylabel('Closing value')

axes[0].set_title('Closing value of Amazon stock')

axes[1].plot(dataset.Date, dataset.Volume, 'c')

axes[1].set_xlabel('Year')

axes[1].set_ylabel('Volume')

axes[1].set_title('Volume of Amazon stock')

axes[2].set_title("Volume vs closing value")

sns.scatterplot(x=dataset.Volume, y=dataset.Close)

plt.tight_layout(pad=2);


#Finding average closing value of Amazon’s stock price in each month

avgtable=np.round(pd.pivot_table(dataset,values="Close", index="Year", columns="Month", aggfunc=np.mean),2)

avgtable


#Making a heatmap of average closing value of Amazon’s stock price in each month

plt.figure(figsize=(12, 6))

plt.title("Average monthly price of Amazon stock")

sns.heatmap(avgtable, cmap="Reds");

#Finding average traded volume of Amazon’s stock price in each month

avgvoltable=np.round(pd.pivot_table(dataset,values="Volume", index="Year", columns="Month", aggfunc=np.mean))

avgvoltable

#Making a heatmap of average traded volume of Amazon’s stock price in each month

plt.figure(figsize=(12, 6))

plt.title("Average monthly traded volume of Amazon stock")

sns.heatmap(avgvoltable, cmap="Greens");



#Finding average yearly closing price of Amazon’s stock

Avgyearlyclosing=np.round(pd.pivot_table(dataset,values="Close", index="Year",aggfunc=np.mean))

Avgyearlyclosing

#Plotting average yearly closing price of Amazon’s stock

plt.figure(figsize=(12, 6))

plt.title("Average yearly closing price")

plt.xlabel("Years")

plt.ylabel("Stock price")

plt.plot(Avgyearlyclosing.index,Avgyearlyclosing.Close, 'r');

#Finding average yearly volume of the stock

Avgyearlyvol=np.round(pd.pivot_table(dataset,values="Volume", index="Year",aggfunc=np.mean))

Avgyearlyvol

#Plotting average yearly volume of the stock

plt.figure(figsize=(12, 6))

plt.title("Average yearly volumes")

plt.xlabel("Years")

plt.ylabel("Volume")

plt.plot(Avgyearlyvol.index,Avgyearlyvol.Volume, 'g');



