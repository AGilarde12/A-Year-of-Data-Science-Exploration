# Summary
Over the week I analyzed 3 datasets:
* Covid data from Bing
* Argentinian Bioethanol Production from the Argentinian Government
* Airbnb data of Venice from Airbnb

# Takeaways
* Day 1 - I learned how to query data directly from a Raw file in github Learned how to quickly visualize and understand a dataset utilizing the head, tail and value count function Sorted and grouped the data by Query, Country, and date to get a better idea of the dataset itself

* Day 2 - I learned how to translate rows and columns using my own knowledge and Google's Translate API and package I learned how to decompose my timeseries data and spot trends I learned how to fit a datetime index to my dataframe to allow for time series analysis I fit/graphed decompositions & ARIMA model, but did not have time in an hour and a half to test

* Day 3 - I learned how write some plotting functions for data inflows using the Seaborns package. I also learned some great and interesting things about the distribution of Room types and Neighbourhood groups in Venice. At the end of the Notebook I tried plot correlation plots and fit a quick regression model. I need to find a better model to handle categorical variables as well

# Functions to use for later

## Distribution Plots
```python
#Function to quickly print the quant. variables in the dataset

#Distribution Plots
def distplot(d):
    import seaborn as sns
    #Empty data for later
    cols = []
        
    #Feature thats int or float in data columns
    for i in d.columns:
        #If the datatypes are = to either below
        if d[i].dtypes == "float64" or d[i].dtypes == "int64":
            #append the columns
            cols.append(i)
    #Define the plot size
    pl = plt.figure(figsize=(10,10))
    #set up the space between the plots
    pl.subplots_adjust(wspace=0.5, hspace=0.5)
    
    #for the range between 1 and the length of the columns + 1
    for i in range(1, len(cols)+1):
        #add a subplot with the parameters below
        ax = pl.add_subplot(3,3,i)
        #using the seaborns package plot the data to a normal fit
        sns.distplot(d[cols[i-1]], fit=norm)
        #set the title as the columns it's plotting
        ax.set_title(format(cols[i-1]))
```
## Correlation Plots

```python
#Function to quickly print corr plots for variables in the dataset


#Correlation plots
def corrplot(d):
    #empty data for later
    cols = []
    
    #Feature thats int or float
    for i in d.columns:
        if d[i].dtypes == "float64" or d[i].dtypes == "int64":
            cols.append(i)

    pl = plt.figure(figsize=(10,10))
    pl.subplots_adjust(wspace=0.5, hspace=0.5)

    for i in range(1, len(cols)+1):
        #uses the joint plot this time to print out each variable from above
        sns.jointplot(x=d['price'], y=d[cols[i-1]], data=d)
```
        
        
