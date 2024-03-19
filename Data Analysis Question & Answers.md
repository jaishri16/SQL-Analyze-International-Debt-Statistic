1. What is the number of distinct countries present in the database? The output should be single column aliased with the following name: total_distinct_countries
```
SELECT COUNT(DISTINCT country_name) AS total_distinct_countries 
FROM international_debt;
```
2. What are the distinct debt indicators? the output column should be aliased as distinct_debt_indicators and the outputs should be ordered by it.
3. What is the total amount of debt owed by all the countries present in the table, in millions? The output should be single column aliased with the following name: total_debt
```
SELECT DISTINCT indicator_name AS distinct_debt_indicators
FROM international_debt
ORDER by distinct_debt_indicators;
```
RESULT:
| distinct_debt_indicators                                    |
|------------------------------------------------------------|
| Disbursements on external debt, long-term (DIS, current US$) |
| Interest payments on external debt, long-term (INT, current US$) |
| Interest payments on external debt, private nonguaranteed (PNG) (INT, current US$) |
| PPG, bilateral (AMT, current US$)                          |
| PPG, bilateral (DIS, current US$)                          |
| PPG, bilateral (INT, current US$)                          |
| PPG, bonds (AMT, current US$)                              |
| PPG, bonds (INT, current US$)                              |
| PPG, commercial banks (AMT, current US$)                   |
| PPG, commercial banks (DIS, current US$)                   |

4. What country has the highest amount of debt?
```
SELECT country_name, sum(debt) AS total_debt
FROM international_debt
GROUP BY country_name
order by total_debt desc
limit 1;
```

RESULT:
| country_name | total_debt       |
|------------------|------------------|
| China            | 285,793,494,734.2 |

5. What is the average amount of debt across different debt indicators?
```
SELECT  indicator_code AS debt_indicator ,indicator_name , avg(debt) as average_debt 
FROM international_debt
GROUP BY indicator_code ,indicator_name
order by average_debt desc
limit 10;
```
RESULT:
| debt_indicator | indicator_name                                                        | average_debt       |
|----------------|----------------------------------------------------------------------|--------------------|
| DT.AMT.DLXF.CD | Principal repayments on external debt, long-term (AMT, current US$) | 5,904,868,401.50  |
| DT.AMT.DPNG.CD | Principal repayments on external debt, private nonguaranteed (PNG) (AMT, current US$) | 5,161,194,333.81 |
| DT.DIS.DLXF.CD | Disbursements on external debt, long-term (DIS, current US$)        | 2,152,041,216.89  |
| DT.DIS.OFFT.CD | PPG, official creditors (DIS, current US$)                          | 1,958,983,452.86  |
| DT.AMT.PRVT.CD | PPG, private creditors (AMT, current US$)                           | 1,803,694,101.96  |
| DT.INT.DLXF.CD | Interest payments on external debt, long-term (INT, current US$)    | 1,644,024,067.65  |
| DT.DIS.BLAT.CD | PPG, bilateral (DIS, current US$)                                   | 1,223,139,290.40  |
| DT.INT.DPNG.CD | Interest payments on external debt, private nonguaranteed (PNG) (INT, current US$) | 1,220,410,844.42 |
| DT.AMT.OFFT.CD | PPG, official creditors (AMT, current US$)                          | 1,191,187,963.08  |
| DT.AMT.PBND.CD | PPG, bonds (AMT, current US$)                                       | 1,082,623,947.65  |

6. What is the highest amount of principal repayments in the "DT.AMT.DLXF.CD" category?
```

SELECT country_name, indicator_name
FROM international_debt
WHERE debt = (SELECT 
                  MAX(debt)
              FROM international_debt
              WHERE indicator_code='DT.AMT.DLXF.CD');
```
RESULT:
| country_name | indicator_name                                                        |
|--------------|----------------------------------------------------------------------|
| China        | Principal repayments on external debt, long-term (AMT, current US$) |

