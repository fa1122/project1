# project1

hello world!

library(class)
library(caret)
library(readxl)
library(party)
library(psych)
library(randomForest)
library(tidyverse)
library(e1071)
library(naivebayes)
data<-read_excel("diagnosis.xlsx", col_names = FALSE)
head(data)
### Eksplorasi data
str(data)
summary(data)

### Ubah tipe variabel menjadi tipe faktor
data$...2 <- as.factor(data$...2)
data$...3 <- as.factor(data$...3)
data$...4 <- as.factor(data$...4)
data$...5 <- as.factor(data$...5)
data$...6 <- as.factor(data$...6)
data$...7 <- as.factor(data$...7)
data$...8 <- as.factor(data$...8)
str(data)


### Split data
Memecah data menjadi data training(80% dari data awal) dan data test (20% dari data awal)
set.seed(1234)
sampel <- sample(2,nrow(data),replace = T, prob = c(0.8,0.2))
trainingdat <- data[sampel==1, ]
testingdat<- data[sampel==2, ]
print(paste("Jumlah Train Data: ", nrow(trainingdat), "| Jumlah Test Data: ", nrow(testingdat)))

trainingdat1<- trainingdat[,-8]
testingdat1<- testingdat[,-8]
trainingdat2<- trainingdat[,-7]
testingdat2<- testingdat[,-7]
head(trainingdat2)

### Membuat Model
## decision tree
pohonnya <- ctree(...7~., data=trainingdat1)
plot(pohonnya)

### Model Evaluation
prediksiDT <- predict(pohonnya, testingdat1)
confusionMatrix(table(prediksiDT,testingdat1$...7))
