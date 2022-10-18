###Susmita Sigdel
###18th October, 2022


#installing package 
install.packages("writexl")
library(writexl)      ###to load the packages

###1.Open the data frame in iris {datasets}. Use the help to know about this data. In
#which units are measured the length and width of sepals and petals? How many 
#variables and observations are there in iris?
do <-iris   #to bring the data frame
?iris  #Units of measurement = centimeters #150 observations # 5 variables 

###2. Create a vector with the species names. Remember that genus should be with 
#capital letters and species in small letters (e.g. “Iris setosa”).
Species <- levels(do$Species)
species <- paste("Iris",levels(do$Species))
species

##3. Create a vector with the name of all quantitative variables
rep(species[1],4)
rep(species[2],4)
rep(species[3],4)
ab <- c(rep(species[1],times=4), rep(species[2],times=4), rep(species[3],times=4))
ab
tn <- rep(names(do[1:4]),3)
tn


###4. Make a data frame with the combination of 
#the two previous vectors like this:
S <- data.frame(species,variable=tn)


###5. Using the data frame from exercise 4, make a data frame with the 
##following variables


####if you want to do it singly the you can use this code
###do <- iris$Species=="setosa"
####mean(iris$Sepal.Length[do])

#Mean
#creating the loop: 
m <- c() ##Empty vector for means 
for (i in levels(iris$Species)) {
  for (j in 1:4) {
   go <- iris$Species==i
   m <- c(m, mean(iris[[j]][go]))
  }}  
m

#standard error
t <- c()   ###Empty vector that keeps the standard error
l <-  length(iris$Species)   ### Number of observaitions 
for (i in levels(iris$Species)) {
  for (j in 1:4) {
    go <- iris$Species==i
    s <- sd(iris[[j]][go])    ##calculate the standard deviation
    standard_error <- s/sqrt(l)  ###calculate the standard error using the formula
    t <- c(t, standard_error)
  }}  
t


#Median 
s <- c()  ###Empty vector that keeps the median
for (i in levels(iris$Species)) {
  for (j in 1:4) {
    go <- iris$Species==i
    s <- c(s, median(iris[[j]][go])) 
  }}
s

#minimum 
y <- c()###Empty vector that keeps the minimum value
for (i in levels(iris$Species)) {
  for (j in 1:4) {
    go <- iris$Species==i
    y <- c(y, min(iris[[j]][go])) 
  }}
y

#maximum value
a <- c() ###Empty vector that keeps the maximum value
for (i in levels(iris$Species)) {
  for (j in 1:4) {
    go <- iris$Species==i
    a <- c(a, max(iris[[j]][go])) 
  }}
a


##make a data frame with the following variables: that is adding the column in the data frame 
S$mean <- m
S$median <- s      ##Adding the colums to the data.frame
S$standard_error <- t
S$minimum_value <- y
S$maximum_value <- a

##6. Install the package “writexl” and use the command write_xlsx to
#create a “yourname.xlsx” file with your data frame.to create excel sheet
p <- "Susmita 1.xlsx"
library(writexl)
write_xlsx(S,p)


