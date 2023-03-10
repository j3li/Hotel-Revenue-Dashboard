# Hotel Revenue Dashboard 

![image](https://user-images.githubusercontent.com/50200083/221953465-e1b95f72-7c47-43f1-b6b1-36aa7455c0ac.png)


[Power BI dashboard](https://app.powerbi.com/view?r=eyJrIjoiOWM5MDQxNzItZDg3My00MTZkLTkzNTEtOWYwNjQ0NTY0Yzk3IiwidCI6IjhhMTk4ODczLTRmZWMtNGU3Ni04MTgyLWNhNDc5ZWRiYmQ2MCIsImMiOjZ9) on hotel revenue and other statistics.
This was used to answer questions such as:
- Is our hotel revenue growing by year?
- Should we increase increase our parking lot size?
  - Are there more customers needing parking?
- What are other trends that we can see?
<br>

**Query used to join tables for analysis and visualization:**
```sql
WITH hotels AS (
SELECT *
FROM dbo.['2018$']
UNION
SELECT *
FROM dbo.['2019$']
UNION
SELECT *
FROM dbo.['2020$']
)

SELECT *
FROM hotels
LEFT JOIN dbo.market_segment$
ON hotels.market_segment = market_segment$.market_segment
LEFT JOIN dbo.meal_cost$
ON meal_cost$.meal = hotels.meal
```

<br>

**Columns & Quick Measures:**
```
Revenue = ([stays_in_week_nights] + [stays_in_weekend_nights])*([adr]*(1-[Discount]))
Total Nights = sum(Query1[stays_in_week_nights]) + sum(Query1[stays_in_weekend_nights])
Parking Percentage = SUM(Query1[required_car_parking_spaces])/[Total Nights]
```
