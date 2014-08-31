##Useful links (essentially what I used to help make this chart) 

[Climate Ecology R and Pandas comparison](http://climateecology.wordpress.com/2014/02/10/a-side-by-side-example-of-r-and-python/)  

[Pandas reference material](http://pandas.pydata.org/pandas-docs/stable/comparison_with_r.html)  

[Yhat, the makers of Python ggplot, have an R and Pandas comparison](http://blog.yhathq.com/posts/R-and-pandas-and-what-ive-learned-about-each.html) 

[As does Wes McKinney](http://pandas.pydata.org/pandas-docs/stable/comparison_with_r.html), the author of Pandas.

##Contents
[Data Structures](#data-structures) 

[Read Data (csv)](#read-data-csv) 

[Read Data (Excel)](#read-data-excel) 

[Clean-Up](#clean-up) 

[Slicing](#slicing) 

[Match](#match) 

[Subset](#subset) 

[Aggregate](#aggregate) 

[Reshape](#reshape) 

[Plotting](#plotting)


**What is R?** R is a general-purpose statistical programming environment. Similar to many programming languages, it has different packages that users have contributed for use with specific functions. R has many packages for analysis and visualization that can be called upon for functions. 

**What is Pandas?** Pandas is a statistical programming library. Like R, Python has many packages contributed by users for specific functions. Pandas is one such library. It is meant to interoperate with different libraries for analysis and visualization.
To use these R functions, simply start R. To use pandas functions, open a Python interpreter and type:

```python
import pandas as pd 
import numpy
```

For information on reading data into R, see [here](https://github.com/datacarpentry/datacarpentry/blob/master/lessons/R/01-starting-with-data.Rmd) and for the same in Pandas, see [here](https://github.com/datacarpentry/datacarpentry/blob/master/lessons/python/01-starting-with-data.md).


###Data Structures

**R**

+ array 
+ list 
+ data.frame

**Python**

+ list
+ Dictionary
+ dataframe (Pandas Package) 


###Read Data (csv)

**R**

```
df <- read.csv('myfile.csv') 
```


**Python**

```python
 df=pd.read_csv('myfile.csv') 
```

###Read Data (Excel)

**R - requires gdata package** 

```
df <- read.xls('myfile.xlsx', sheet = 1, header = TRUE) 
```

**Python**

```python
xl = pandas.ExcelFile('myfile.xlsx') 
df = xl.parse('Sheet1')
```

###Clean-Up

**R**

Drop incomplete data

```
weight <- subset(df, !is.na(wgt))
```

Fixing data errors

```
df$temp[which(df$wgt==45)]<-42
```

**Python**

Drop incomplete data

```python
weight=df.dropna(subset=['wgt'])
```

Fixing data errors

```python
df['wgt'].replace(45, 42, inplace=True)
```


###Slicing

**R** 

Access columns by name

``` 
df[, c( 'a', 'b', 'c')] 
```

Access columns by location

```
df[, c(1:10, 35:40)] 
```


**Python**

Access columns by name
```python
df[['a', 'b', 'c']] 
```

or

```python
df.loc[ : , ['a', 'b', 'c']]
```

Select multiple, noncontinguous, columns by location--use .iloc and numpy.r

```python
df.iloc[ : , np.r_[:10, 35:40]]
```

##Match

Select data using %in%, which returns logical vector indicating if there is a match or not

**R**

```
g %in% c(1,10)

```

Return vector of match positions

```
match(g, c(1,10))
```

**Python**

Return vector of match positions

```python
g.isin([2,4])
```

Apply() method to return a pandas series object (a similar object to an R vector) of matches

```python
pd.Series(pd.match(g,[1,10], np.nan)
```


##Subset

**R** 

Get rows of dataframe that satisfy some statement

```
subset(df, wgt <= 100)
```

```
spec <- c('elephant', 'giraffe','ostrich')
sub_dat <- [df$species %in% species, ]
```


**Python** 

Get rows of dataframe that satisfy some statement using the query() method 

```python
df. query('weight' <= 100) 
```

Subsetting with standard slicing

```python
subset = df[df.wgt <= 100] 
```
or

```python
df.loc[df.weight <=100]
```

Fancy subsetting with matching

```python
spec=['elephant', 'giraffe', 'ostrich']
sub_dat=df[species['species'].isin(spec)] 
```

##Aggregate

**R**

Aggregate function to split data and compute means for each   
```
aggregate(x=df[, c('v1', 'v2')], by=list(mydf2$by1, mydf2$by2), FUN=mean) 
```

Tapply is similar to aggregate but can be used on ragged arrays

```
tapply(animals$avg_wgt,animals$sex, mean) 
```

**Python**

grouby() method groups data by some facet or facets of the dataset.

```python
g=df.grouby(['by1', 'by2'])
```

Pivot_table() method is pandas equivalent of tapply 

```python
animals.pivot_table(values='wgt', columns='sex', aggfunc=np.mean)
```

###Reshape

**R** 

reshape2 package to switch data between wide and long formats 

`melt` can be used to reshape lists to dataframes	

```
data.frame(melt(a))				
```

`melt.data.frame` to reshape an existing dataframe

```
melt(df, id=('a', 'b'))
```

**Python**

Dataframe method to convert between non-data frame objects and data frames
```python
DataFrame(a)  
```

Melt method for transforming multiple list to data frames

```python
pd.melt(df, id_vars=['a', 'b']) 
```

###Plotting

**R** 

+ Native: plot, hist, boxplot             
+ Other popular packages: ggplot2						

   
**Python**

+ Native: hist, plot, boxplot
+ Other popular packages: Matplotlib, ggplot2
