library(haven)
library(dplyr)
library(dbplyr)
library(RSQLite)
library(DBI)

tax <- read.csv("Council_Tax1.csv", header = T)
house <- read.csv("House_Prices.csv", header = T)
speed <- read.csv("Internet_Speed1.csv", header = T)
ward <- read.csv("Ward.csv", header = T)

conn <- dbConnect(SQLite(),"DF3.db")

dbCreateTable(conn, "Ward", ward)
dbCreateTable(conn, "Internet_Speed", speed)
dbCreateTable(conn, "House_Prices", house)
dbCreateTable(conn, "Council_Tax", tax)

dbAppendTable(conn, "Ward", ward)
dbAppendTable(conn, "Internet_Speed", speed)
dbAppendTable(conn, "House_Prices", house)
dbAppendTable(conn, "Council_Tax", tax)

#Query 1(Quest.3)
q1 <- dbGetQuery(conn, 'SELECT YearendingDec2015, YearendingMar2015, YearendingJun2015, YearendingSep2015, YearendingDec2016, YearendingMar2016, YearendingJun2016, YearendingSep2016 FROM House_Prices INNER JOIN Ward ON Ward.Wardcode = House_Prices.Wardcode WHERE Ward.WardName = "Thame"')

meanYHprice <- mean(as.numeric(q1[1,]))
meanYHprice
#318153.1

#Query 2(Quest.4)
#We can use the same prices as question 1.

pric15 <- as.numeric(q1[1,1:4])
pric16 <- as.numeric(q1[1,5:8])
mean15 <- mean(pric15)
mean16 <- mean(pric16)

pcAvgInc <- ((mean16/mean15)-1) * 100
pcAvgInc <- paste(as.character(pcAvgInc),"%")
pcAvgInc
#22.9719 % Increase

#Query 3(Quest.5)
q3 <- dbGetQuery(conn, 'SELECT WardName FROM Ward INNER JOIN House_Prices ON Ward.Wardcode = House_Prices.Wardcode WHERE House_Prices.YearendingMar2004 = (SELECT max(YearendingMar2004) FROM House_Prices)')
q3
#Holywell has the max price for march/2004

#Query 4(Quest.6)
q4 <- dbGetQuery(conn, 'SELECT Avg_DownloadSpeedMbs FROM Ward INNER JOIN Internet_Speed ON Ward.Wardcode = Internet_Speed.Wardcode WHERE Ward.WardName = "Bicester West"')
q4
#62 Mb/s for Bicester West

#Query 5 (Quest.7)
#We would like to see which ward has the greatest percentage.
#Of connections with super fast speed.
#Crucial info for a user looking to get easily a high speed connection.

q5 <- dbGetQuery(conn, 'SELECT WardName FROM Ward INNER JOIN Internet_Speed ON Ward.Wardcode = Internet_Speed.Wardcode WHERE Internet_Speed.ConnectionsReceivingSuperfastSpeeds = (SELECT max(ConnectionsReceivingSuperfastSpeeds) FROM Internet_Speed)')
q5
#Marston has the highest percentage of high speed connections.

#Query 6 (Quest.8)
q6 <- dbGetQuery(conn, 'SELECT Band_F, Band_G, Band_H FROM Council_Tax WHERE Council_Tax.Town = "Littlemore"')
meanofBands <- mean(as.numeric(q6[1,]))
meanofBands
#The mean of bands F,G and H for the city of Littlemore is £3695.727

#Query 7 (Quest.9)
q9a <- dbGetQuery(conn, 'SELECT Band_A FROM Council_Tax WHERE Council_Tax.Town = "Claydon"')
q9b <- dbGetQuery(conn, 'SELECT Band_A FROM Council_Tax WHERE Council_Tax.Town = "Prescote"')
claydonA <- as.numeric(q9a[1,1])
prescoteA <- as.numeric(q9b[1,1])


diffA <- claydonA - prescoteA
diffA
#Claydon's Band A has £53.53 more expensive council tax
#From Prescote's Band A.


dbDisconnect(conn)
