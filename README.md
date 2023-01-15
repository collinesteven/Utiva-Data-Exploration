## MANIPULATION OF THE DATA

The analysis were divided into three sections which are;

a. Profit Analysis

b. Brand Analysis

c. Countries Analysis

## Profit Analysis

Firstly, In generating insights on Profit analysis, profit, countries, years and months were taking into consideration as they help get understand of the location and period. 
There are several questions that need answers in this analysis which are below:

 --  Within the space of the last three years, what was the profit worth of the breweries, inclusive of the anglophone and the francophone territories?
 
  ```SQL
 SELECT years,
        brands,
        region as "Territories",
        SUM(profit) as "Total Profit"
FROM internationalbreweries.pabod
GROUP BY years,brands,region
ORDER BY years DESC
 ```
 
--  Compare the total profit between these two territories in order for the territory manager, Mr. Stone made a strategic decision that will aid profit maximization in 2020.

```SQL
 SELECT region as "Territories",
        SUM(profit) as "Total Profit"
 FROM internationalbreweries.pabod
 GROUP BY region
 ORDER BY "Total Profit" DESC
 ```

-- Country that generated the highest profit in 2019
 
 ```SQL
 SELECT years,
        countries,
        SUM(profit) as "Total Profit" 
FROM internationalbreweries.pabod
WHERE years ='2019'
GROUP BY years,countries
ORDER BY "Total Profit" DESC 
```

-- Help him find the year with the highest profit.
  ```SQL
  SELECT years,
         SUM(profit) as "Total Profit" 
FROM internationalbreweries.pabod
GROUP BY years
ORDER BY "Total Profit" DESC
```

-- Which month in the three years was the least profit generated?
  ```SQL
  SELECT years,
         months,
         SUM(profit) as "Total Profit" 
FROM internationalbreweries.pabod
GROUP BY years,months
ORDER BY "Total Profit" ASC
```

-- What was the minimum profit in the month of December 2018?
  ```SQL
  SELECT years,
         months,
         MIN(profit) as "minimum profit"
FROM internationalbreweries.pabod
WHERE months='December'AND years='2018'
GROUP BY years,months
ORDER BY MIN(profit) ASC
```

-- Which particular brand generated the highest profit in Senegal?
     
  ```SQL 
  SELECT brands,
         countries,
         SUM(profit) as "Total Profit" 
FROM internationalbreweries.pabod
WHERE countries='Senegal'
GROUP BY brands,countries
ORDER BY  "Total Profit"  DESC
```

 ## Brand Analysis
     
The brand analysis entails the brand usage by customers in all the regions.The questions here focus more on brands, customer and quantity. 


  -- Within the last two years, the brand manager wants to know the top three brands consumed in the francophone countries
    
  ```SQL 
  SELECT years,
         brands,
         countries,
         SUM(quantity) as "Total Quantity"
FROM internationalbreweries.pabod
WHERE countries!='Nigeria' AND countries!='Ghana' AND years!='2017'
GROUP BY years,brands,countries
ORDER BY "Total Quantity" DESC
```

-- Find out the top two choice of consumer brands in Ghana
   
   
   ```SQL
   SELECT brands,
          countries,
          SUM(quantity) as "Total Quantity"
FROM internationalbreweries.pabod
WHERE countries ILIKE 'Ghana'
GROUP BY brands,countries
ORDER BY "Total Quantity" ```
```

--  Find out the details of beers consumed in the past three years in the most oil reached country in West Africa.
    
    
  ```SQL
  SELECT *
FROM internationalbreweries.pabod
WHERE countries ILIKE 'Nigeria'
```

-- Favorites malt brand in Anglophone region between 2018 and 2019
   
   
 ```SQL
 SELECT years,
        brands,
        region,
        countries
FROM internationalbreweries.pabod
WHERE years BETWEEN '2018' AND '2019' AND brands ILIKE '%malt' 
OR region ILIKE 'northeast' OR region ILIKE 'northwest' OR region ILIKE 'northcentral' OR region ILIKE 'southsouth' 
OR region ILIKE 'southeast' OR region ILIKE 'west'
```

-- Which brands sold the highest in 2019 in Nigeria?

```SQL
SELECT years,
       brands,
       countries,
       SUM(quantity) as "Total Quantity"
FROM internationalbreweries.pabod
WHERE years='2019' AND countries ILIKE 'Nigeria'
GROUP BY years,brands,countries
ORDER BY "Total Quantity" DESC
```

-- Favorites brand in South_South region in Nigeria

```SQL
SELECT brands,
       region,
       countries
FROM internationalbreweries.pabod
WHERE region ILIKE'southsouth' AND countries = 'Nigeria'
```

-- Bear consumption in Nigeria

```SQL
SELECT years,
       brands,
       months,
       countries,
       SUM(quantity) as "Total Quantity"
FROM internationalbreweries.pabod
WHERE countries='Nigeria'
GROUP BY years,brands,months,countries
ORDER BY years DESC,months ASC
```

-- Level of consumption of Budweiser in the regions in Nigeria

```SQL
SELECT years,
       months,
       brands,
       region,
       countries,
       SUM(quantity) as "Total Quanity"
FROM internationalbreweries.pabod
WHERE brands ILIKE 'Budweiser'AND countries ILIKE 'Nigeria'
GROUP BY  years,months,brands,region,countries
ORDER BY years ASC
```

-- Level of consumption of Budweiser in the regions in Nigeria in 2019 (Decision on Promo)

```SQL
SELECT years,
       months,
       brands,
       region,
       countries,
       SUM(quantity) as "Total Quanity"
FROM internationalbreweries.pabod
WHERE years='2019' AND brands ILIKE 'Budweiser'AND countries ILIKE 'Nigeria'
GROUP BY years,months,brands,region,countries
ORDER BY years ASC
```

## Countries Analysis

The main analysis will be centered on country profit and the personnel in these countries. Sales representatives will also serve as metric in measuring number of quantities sold. 

-- Country with the highest consumption of beer.
```Sql
SELECT countries,
		SUM(quantity) AS consump_quantities
FROM International_breweries.pabod
WHERE brands NOT LIKE '%Malt%'
GROUP BY 1
ORDER BY 2 DESC
LIMIT 1
```

-- Highest sales personnel of Budweiser in Senegal

```sql
SELECT sales_rep,
       SUM(quantity) as sales
FROM international_breweries.pabod
WHERE brands = 'budweiser' 
	AND countries ='Senegal'
GROUP BY 1
ORDER BY 2 DESC
LIMIT 5;
```

--Country with the highest profit of the fourth quater in 2019

```SQL
SELECT countries,
	SUM(profit) AS profit
FROM International_breweries.pabod
WHERE months IN ('october','November','December')
	AND years = '2019'
GROUP BY 1
ORDER BY 2 DESC
LIMIT 3:
```
