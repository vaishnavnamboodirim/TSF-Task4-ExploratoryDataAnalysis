#The Spark Foundation Internship
#Name : Vaishnav Nmaboodiri M
#Exploratory Data Analysis - Terrorism (Level - Intermediate) 
# Perform ‘Exploratory Data Analysis’ on dataset ‘Global Terrorism’.As a defense analyst, try to,
#find out the hot zone of terrorism.  
# What all security issues and insights you can derive by EDA?

library(ggplot2)
library(cluster)
library(tidyverse)
library(factoextra)
require("datasets")

setwd("C:/Users/acer/Desktop/DataAnalytics")
getwd()
data <- fread("globalterrorismdb_0718dist.csv") 
a<-data %>% group_by(region_txt) %>% summarise(n=n())
a<-a %>% arrange(-n)
ggplot(a,aes(x=region_txt,y=n)) + geom_bar(stat="identity",fill="#FF6666") + theme(axis.text.x=element_text(angle = 90,hjust = 1,vjust = 0.5)) + scale_fill_manual(values = c("#FF6666"))


b<-data %>% filter(iyear=="1970") %>%group_by(region_txt) %>% summarise(n=n())
ggplot(b,aes(x=region_txt,y=n)) + geom_bar(stat = "identity",fill="#FF6666") + theme(axis.text.x=element_text(angle = 90,hjust = 1,vjust = 0.5))

c<-data %>% filter(iyear>="1970" & iyear <= "1980") %>%group_by(region_txt) %>% summarise(n=n())
ggplot(c,aes(x=region_txt,y=n)) + geom_bar(stat="identity",fill="#FF6666") +  theme(axis.text.x=element_text(angle = 90,hjust = 1,vjust = 0.5))
install.packages("janitor")
library(janitor)

d<-data %>% filter(iyear>="1970" & iyear <= "2000") %>%group_by(region_txt) %>% summarise(n=n())
ggplot(d,aes(x=region_txt,y=n)) + geom_bar(stat="identity",fill="#FF6666") + theme(axis.text.x=element_text(angle = 90,hjust = 1,vjust = 0.5))

data %>% filter(iyear>="2001" & iyear <= "2017") %>%group_by(iyear,region_txt) %>% summarise(n=n())
ggplot(data,aes(x=region_txt)) + geom_bar() + theme(axis.text.x=element_text(angle = 90,hjust = 1,vjust = 0.5))

e<-data%>% filter(iyear == "2017") %>%group_by(region_txt) %>% summarise(n=n())
ggplot(e,aes(x=region_txt,y=n)) + geom_bar(stat = "identity",fill="#FF6666") + theme(axis.text.x=element_text(angle = 90,hjust = 1,vjust = 0.5))

f<-data %>% filter(region_txt == "Middle East & North Africa") %>%group_by(country_txt) %>% summarise(n=n())
f %>% arrange(-n)
ggplot(f,aes(x=country_txt,y=n)) + geom_bar(stat="identity",fill="#FF6666") + theme(axis.text.x=element_text(angle = 90,hjust = 1,vjust = 0.5))

G<-data %>% filter(region_txt == "Middle East & North Africa")%>% select(iyear,nkill) %>%group_by(iyear) %>% summarise(n=n())
G
ggplot(G, aes(x=iyear,y=n,group=1))+ geom_line() + geom_point()


H<-data %>% select(attacktype1_txt) %>% group_by(attacktype1_txt) %>% na.omit() %>% summarise(n=n())
ggplot(H,aes(x=attacktype1_txt,y=n)) + geom_bar(stat="identity",fill="#FF6666") + theme(axis.text.x=element_text(angle = 90,hjust = 1,vjust = 0.5))

i<-data %>% select(attacktype2_txt) %>% group_by(attacktype2_txt) %>% na.omit() %>% summarise(n=n())
head(data)
ggplot(i,aes(x=attacktype2_txt,y=n)) + geom_bar(stat="identity",fill="#FF6666") + theme(axis.text.x=element_text(angle = 90,hjust = 1,vjust = 0.5))


j<-data %>% select(targtype1_txt) %>% group_by(targtype1_txt) %>% na.omit() %>% summarise(n=n())
ggplot(j,aes(x=targtype1_txt,y=n)) + geom_bar(stat="identity",fill="#FF6666") + theme(axis.text.x=element_text(angle = 90,hjust = 1,vjust = 0.5))

k<-data %>% select(weaptype1_txt) %>% group_by(weaptype1_txt) %>% na.omit() %>% summarise(n=n())
ggplot(k,aes(weaptype1_txt,y=n)) + geom_bar(stat="identity") + theme(axis.text.x=element_text(angle = 90,hjust = 1,vjust = 0.5))

l<-data %>% select(dbsource) %>% group_by(dbsource) %>% na.omit() %>% summarise(n=n())
ggplot(l,aes(x=dbsource,y=n)) + geom_bar(stat="identity",fill="#FF6666") + theme(axis.text.x=element_text(angle = 90,hjust = 1,vjust = 0.5))

m<-data %>% select(gname) %>% group_by(gname) %>% na.omit() %>% summarise(n=n()) %>% arrange(desc(n))
m<-m %>%filter(!str_detect(gname,'Unknown'))
m<-m %>% top_n(20)
ggplot(m, aes(x=gname,y=n))+ geom_bar(stat="identity",fill="#FF6666") +  theme(axis.text.x=element_text(angle = 90,hjust = 1,vjust = 0.5))


Q<-data %>% filter(region_txt == "Middle East & North Africa") %>%group_by(country_txt) %>% summarise(n=n()) %>% arrange(desc(n))
Q$n <- as.numeric(Q$n)
head(Q)
barplot(height = Q$n, names = Q$country_txt,col="#69b3a2",las=2)


