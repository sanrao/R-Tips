# R-Tips
Interesting R tips and tricks

############### Updating R while using Rstudio

# installing/loading the package:
if(!require(installr)) {
  install.packages("installr"); require(installr)} #load / install+load installr

# using the package:
updateR() # this will start the updating process of your R installation.  It will check for newer versions, and if one is available, will guide you through the decisions you'd need to make.

#Restart R studio update is complete

################ My understanding of R datetime Conversions

#Datetime formats are very important for most transportation projects. 

#R uses two classes for representing timestamps:
#1. POSIXct and 2. POSIXlt
https://stat.ethz.ch/R-manual/R-devel/library/base/html/DateTimeClasses.html

#functions used to convert to these classes are called as.POSIXct and as.POSIXlt

#strptime function converts between character representation and objects of classes POSIXct and (POSIXithttps://stat.ethz.ch/R-manual/R-devel/library/base/html/strptime.html)

#Examples
DT <-DT[,`:=`(timestamp= as.POSIXct(strptime("2015-11-07 22:01:43", "%Y-%m-%d %H:%M:%S")))]

#The trick is to use string function to assimilate all the date and time information into the first argument of strptime and then 
#define the correct formation in the second argument.

#Additional links:
#http://www.statmethods.net/input/dates.html
#https://stat.ethz.ch/R-manual/R-devel/library/base/html/strptime.html

################ My understanding of fread function

#select
Vector of column names or numbers to keep, drop the rest.

#Use colClasses argument if you need to customize how a particular column is read into your data.table.  This helps especially with 
date and time variables wher the original data is stored in the numeric format.

#Example:

load_data <- function(path) {
  files <-dir(path, pattern = '\\-data.txt', full.names  = TRUE)
  tables <-lapply(files, function(i){fread(i,colClasses=c("integer","character","integer","character","character"))})
  do.call(rbind,tables)
}

#The input data format was the following

Number BluetoothID      v3        Date      Time
3165	A0:40:41:02:02:2F	5.125516	20151103	200000
3166	00:00:00:00:00:00	5.125778	20151103	200005
3167	00:00:00:00:00:00	5.126396	20151103	200011
3168	00:1E:B2:95:C1:53	5.126376	20151103	200013
9866	10:C6:FC:DC:B2:57	5.125904	20151104	060134
9866	14:8F:21:1C:36:E8	5.125904	20151104	060137
9866	B4:B6:76:27:FA:AF	5.125904	20151104	060137

#Which is why for the sake of consistency the Time variable had to be imported as a character

################ Rounding Functions in R

#Two functions that I use floor(x) and round(x, digits=n).
#Floor of course moves down the number to the nearest integer while the round function moves it to the nearest integer (higher or low)
#Used it for extracting year, month, day from a integer of the form 20150723

################ Will update about the lead lag (shift) variable tomorrow























