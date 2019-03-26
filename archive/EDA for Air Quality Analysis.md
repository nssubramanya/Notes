# EDA for Air Quality Analysis
### Use Command line tools can be used to view parts of the file

```
$ head <filename>  
$ tail <filename>  
$ grep <RegExp> <filename>
```

### Look at the header line
* Is a header present?
* What is the Field Separator?
* What is the Comment Character
* How are missing values represented?

### Reading the file
```{r}
df <- read.table (file="", header="", comment.char="", sep="", na.strings="")

```

### Dimensioning
* Check dimensions of file - Number of Observations & Columns

``` {r}
dim(df)

```
* Check the first & last few lines

```{r}
head(df)
tail(df)
```

* Check the type of variables

```{r}
str(df)
summary(df)
```

* Get the names of the column Headings

```{r}

```
