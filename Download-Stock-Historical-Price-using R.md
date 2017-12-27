---
title: Download Stock Historical Price using R
date: 2017-12-25 21:27:55
categories: stock
tags: stock
---
关于美股历史价格的下载， 之前很多人一直用Yahoo API，今年年初时候Yahoo API不好用了，各路神仙开始另寻他法。网上search一圈，觉得用R里面的package tidyquant 下载SP500的历史数据算比较方便的，代码如下

     install.packages("tidyquant")
     library(tidyquant)
     sp500<-tq_index("sp500")%>%tq_get(get="stock.prices")

the sp500 data downloaded this way is a big data. Since R is not good at dealing with big data, I splited the download into three parts by the following way

     sp01<-tq_index("sp500")%>%tq_get(get="stock.prices",from="2007-01-01,to="2010-12-31")
     SP1=sp01[complete.cases(sp01),]  #remove all 'NA' values
     write.csv(sp1,file="c:/sp1.csv",row.names = FALSE) #prevent row names being writen to file

     sp02<-tq_index("sp500")%>%tq_get(get="stock.prices",from="2011-01-01",to="2013-12-31")
     SP2=sp02[complete.cases(sp02),]
     write.csv(sp2,file="c:/sp2.csv",row.names = FALSE)

     sp03<-tq_index("sp500")%>%tq_get(get="stock.prices",from="2014-01-01",to="2017-12-31")
     SP3=sp03[complete.cases(sp03),]
     write.csv(sp3,file="c:/sp3.csv",row.names = FALSE)




