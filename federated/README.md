[root@sandbox ~]# echo "zeppelin ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
[root@sandbox ~]# echo "host all all 127.0.0.1/32 md5" >> /var/lib/pgsql/data/pg_hba.conf

[root@sandbox ~]# sudo su - zeppelin
-bash-4.1$ cd /tmp
-bash-4.1$ wget  https://www.dropbox.com/s/r70i8j1ujx4h7j8/data.zip
--2016-05-03 23:23:28--  https://www.dropbox.com/s/r70i8j1ujx4h7j8/data.zip
Resolving www.dropbox.com... 162.125.4.1
Connecting to www.dropbox.com|162.125.4.1|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://dl.dropboxusercontent.com/content_link/a0JsrG40VDd3GsOD8DgRKsUrUmTQ09Lm4owu0wSvimTQjhult1XT2yEBOH0AOppH/file [following]
--2016-05-03 23:23:28--  https://dl.dropboxusercontent.com/content_link/a0JsrG40VDd3GsOD8DgRKsUrUmTQ09Lm4owu0wSvimTQjhult1XT2yEBOH0AOppH/file
Resolving dl.dropboxusercontent.com... 45.58.70.5
Connecting to dl.dropboxusercontent.com|45.58.70.5|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 544623675 (519M) [application/zip]
Saving to: “data.zip”

100%[====================================================================================================================================================>] 544,623,675 61.7M/s   in 9.2s

2016-05-03 23:23:38 (56.6 MB/s) - “data.zip” saved [544623675/544623675]

-bash-4.1$ unzip data.zip
Archive:  data.zip
  inflating: data/DimAccount.csv
  inflating: data/DimChannel.csv
  inflating: data/DimCurrency.csv
  inflating: data/DimCustomer.csv
  inflating: data/DimDate.csv
  inflating: data/DimEmployee.csv
  inflating: data/DimEntity.csv
  inflating: data/DimGeography.csv
  inflating: data/DimMachine.csv
  inflating: data/DimOutage.csv
  inflating: data/DimProduct.csv
  inflating: data/DimProductCategory.csv
  inflating: data/DimProductSubcategory.csv
  inflating: data/DimPromotion.csv
  inflating: data/DimSalesTerritory.csv
  inflating: data/DimScenario.csv
  inflating: data/DimStore.csv
  inflating: data/FactExchangeRate.csv
  inflating: data/FactInventory.csv
  inflating: data/FactITMachine.csv
  inflating: data/FactITSLA.csv
  inflating: data/FactOnlineSales.csv
  inflating: data/FactSales.csv
  inflating: data/FactSalesQuota.csv

  inflating: data/FactStrategyPlan.csv
-bash-4.1$ head /tmp/data/FactSales.csv
SalesKey,DateKey,channelKey,StoreKey,ProductKey,PromotionKey,CurrencyKey,UnitCost,UnitPrice,SalesQuantity,ReturnQuantity,ReturnAmount,DiscountQuantity,DiscountAmount,TotalCost,SalesAmount,ETLLoadID,LoadDate,UpdateDate
1,2007-01-02 00:00:00,1,209,956,10,1,91.05,198,8,0,0,1,39.6,728.4,1544.4,1,2010-01-01 00:00:00,2010-01-01 00:00:00
2,2007-02-12 00:00:00,4,308,766,2,1,10.15,19.9,4,0,0,1,0.995,40.6,78.605,1,2010-01-01 00:00:00,2010-01-01 00:00:00
3,2008-01-24 00:00:00,1,156,1175,11,1,209.03,410,9,0,0,3,61.5,1881.27,3628.5,1,2010-01-01 00:00:00,2010-01-01 00:00:00
4,2008-01-13 00:00:00,2,306,1429,10,1,132.9,289,8,0,0,1,57.8,1063.2,2254.2,1,2010-01-01 00:00:00,2010-01-01 00:00:00
5,2008-01-22 00:00:00,2,306,1133,10,1,144.52,436.2,24,0,0,3,261.72,3468.48,10207.08,1,2010-01-01 00:00:00,2010-01-01 00:00:00
6,2007-07-02 00:00:00,3,200,2365,3,1,183.94,399.99,36,0,0,10,399.99,6621.84,13999.65,1,2010-01-01 00:00:00,2010-01-01 00:00:00
7,2007-11-19 00:00:00,4,310,1016,5,1,68.06,148,6,0,0,2,44.4,408.36,843.6,1,2010-01-01 00:00:00,2010-01-01 00:00:00
8,2008-04-10 00:00:00,2,307,138,15,1,229.93,499.99,9,0,0,1,99.998,2069.37,4399.912,1,2010-01-01 00:00:00,2010-01-01 00:00:00
[root@sandbox ~]# pwd
/root
[root@sandbox ~]# sudo su - zeppelin
-bash-4.1$ cd /tmp
-bash-4.1$ wget  https://www.dropbox.com/s/r70i8j1ujx4h7j8/data.zip
--2016-05-03 23:23:28--  https://www.dropbox.com/s/r70i8j1ujx4h7j8/data.zip
Resolving www.dropbox.com... 162.125.4.1
Connecting to www.dropbox.com|162.125.4.1|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://dl.dropboxusercontent.com/content_link/a0JsrG40VDd3GsOD8DgRKsUrUmTQ09Lm4owu0wSvimTQjhult1XT2yEBOH0AOppH/file [following]
--2016-05-03 23:23:28--  https://dl.dropboxusercontent.com/content_link/a0JsrG40VDd3GsOD8DgRKsUrUmTQ09Lm4owu0wSvimTQjhult1XT2yEBOH0AOppH/file
Resolving dl.dropboxusercontent.com... 45.58.70.5
Connecting to dl.dropboxusercontent.com|45.58.70.5|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 544623675 (519M) [application/zip]
Saving to: “data.zip”

100%[====================================================================================================================================================>] 544,623,675 61.7M/s   in 9.2s

2016-05-03 23:23:38 (56.6 MB/s) - “data.zip” saved [544623675/544623675]

-bash-4.1$ unzip data.zip
Archive:  data.zip
  inflating: data/DimAccount.csv
  inflating: data/DimChannel.csv
  inflating: data/DimCurrency.csv
  inflating: data/DimCustomer.csv
  inflating: data/DimDate.csv
  inflating: data/DimEmployee.csv
  inflating: data/DimEntity.csv
  inflating: data/DimGeography.csv
  inflating: data/DimMachine.csv
  inflating: data/DimOutage.csv
  inflating: data/DimProduct.csv
  inflating: data/DimProductCategory.csv
  inflating: data/DimProductSubcategory.csv
  inflating: data/DimPromotion.csv
  inflating: data/DimSalesTerritory.csv
  inflating: data/DimScenario.csv
  inflating: data/DimStore.csv
  inflating: data/FactExchangeRate.csv
  inflating: data/FactInventory.csv
  inflating: data/FactITMachine.csv
  inflating: data/FactITSLA.csv
  inflating: data/FactOnlineSales.csv
  inflating: data/FactSales.csv
  inflating: data/FactSalesQuota.csv

  inflating: data/FactStrategyPlan.csv
-bash-4.1$ head /tmp/data/FactSales.csv
SalesKey,DateKey,channelKey,StoreKey,ProductKey,PromotionKey,CurrencyKey,UnitCost,UnitPrice,SalesQuantity,ReturnQuantity,ReturnAmount,DiscountQuantity,DiscountAmount,TotalCost,SalesAmount,ETLLoadID,LoadDate,UpdateDate
1,2007-01-02 00:00:00,1,209,956,10,1,91.05,198,8,0,0,1,39.6,728.4,1544.4,1,2010-01-01 00:00:00,2010-01-01 00:00:00
2,2007-02-12 00:00:00,4,308,766,2,1,10.15,19.9,4,0,0,1,0.995,40.6,78.605,1,2010-01-01 00:00:00,2010-01-01 00:00:00
3,2008-01-24 00:00:00,1,156,1175,11,1,209.03,410,9,0,0,3,61.5,1881.27,3628.5,1,2010-01-01 00:00:00,2010-01-01 00:00:00
4,2008-01-13 00:00:00,2,306,1429,10,1,132.9,289,8,0,0,1,57.8,1063.2,2254.2,1,2010-01-01 00:00:00,2010-01-01 00:00:00
5,2008-01-22 00:00:00,2,306,1133,10,1,144.52,436.2,24,0,0,3,261.72,3468.48,10207.08,1,2010-01-01 00:00:00,2010-01-01 00:00:00
6,2007-07-02 00:00:00,3,200,2365,3,1,183.94,399.99,36,0,0,10,399.99,6621.84,13999.65,1,2010-01-01 00:00:00,2010-01-01 00:00:00
7,2007-11-19 00:00:00,4,310,1016,5,1,68.06,148,6,0,0,2,44.4,408.36,843.6,1,2010-01-01 00:00:00,2010-01-01 00:00:00
8,2008-04-10 00:00:00,2,307,138,15,1,229.93,499.99,9,0,0,1,99.998,2069.37,4399.912,1,2010-01-01 00:00:00,2010-01-01 00:00:00
9,2008-07-14 00:00:00,2,199,1731,12,1,33.32,72.45,24,0,0,5,36.225,799.68,1702.575,1,2010-01-01 00:00:00,2010-01-01 00:00:00

