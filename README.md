### 📊 Data Transformation Cheat Sheet (Python | SQL | DAX)

---

| Transformation             | Python (Pandas)                                                   | SQL                                                            | DAX                                                                        |
| -------------------------- | ----------------------------------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------------------- |
| **Filter & Sort Rows**     | `df[df["salary"] > 50000].sort_values("salary", ascending=False)` | `SELECT * FROM emp WHERE salary > 50000 ORDER BY salary DESC;` | `FILTER(Emp, Emp[salary] > 50000)`                                         |
| **Pivot**                  | `df.pivot(index="date", columns="region", values="sales")`        | `PIVOT (SUM(sales) FOR region IN ('US','EU'))`                 | `SUMMARIZE(Sales, Sales[date], Sales[region], "Total", SUM(Sales[sales]))` |
| **Merge / Join**           | `pd.merge(df1, df2, on="id", how="left")`                         | `SELECT * FROM a LEFT JOIN b ON a.id=b.id;`                    | `NATURALLEFTOUTERJOIN(A, B)`                                               |
| **Append / Union**         | `pd.concat([df1, df2])`                                           | `SELECT * FROM a UNION ALL SELECT * FROM b;`                   | `UNION(TableA, TableB)`                                                    |
| **Trim & Case**            | `df["name"].str.strip().str.upper()`                              | `SELECT TRIM(UPPER(name)) FROM t;`                             | `TRIM(UPPER(Table[name]))`                                                 |
| **Handle Missing Values**  | `df["score"].fillna(0)`                                           | `SELECT COALESCE(score,0) FROM t;`                             | `IF(ISBLANK(T[score]),0,T[score])`                                         |
| **Remove Duplicates**      | `df.drop_duplicates()`                                            | `SELECT DISTINCT * FROM t;`                                    | `DISTINCT(Table)`                                                          |
| **Group By / Aggregation** | `df.groupby("dept")["salary"].avg()`                              | `SELECT dept, AVG(salary) FROM emp GROUP BY dept;`             | `AVERAGE(Emp[salary])`                                                     |
| **Having / Agg Filter**    | `df.groupby("dept").filter(lambda x: x.salary.mean()>50000)`      | `HAVING AVG(salary) > 50000`                                   | `FILTER(VALUES(Emp[dept]), [AvgSalary]>50000)`                             |
| **Ranking**                | `df["rank"]=df["sales"].rank(desc=True)`                          | `RANK() OVER(ORDER BY sales DESC)`                             | `RANKX(ALL(Sales), SUM(Sales[sales]))`                                     |
| **Top N**                  | `df.nlargest(5,"sales")`                                          | `ORDER BY sales DESC LIMIT 5`                                  | `TOPN(5, Sales, Sales[sales], DESC)`                                       |
| **Conditional Column**     | `np.where(df["score"]>=60,"Pass","Fail")`                         | `CASE WHEN score>=60 THEN 'Pass' ELSE 'Fail' END`              | `IF(T[score]>=60,"Pass","Fail")`                                           |
| **Date Functions**         | `df["year"]=pd.to_datetime(df["date"]).dt.year`                   | `YEAR(order_date)`                                             | `YEAR(Table[date])`                                                        |
| **Text Parsing**           | `df["code"]=df["id"].str[:3]`                                     | `SUBSTRING(id,1,3)`                                            | `LEFT(Table[id],3)`                                                        |
| **Numeric Calc**           | `df["x"].round(2)`                                                | `ROUND(x,2)`                                                   | `ROUND(Table[x],2)`                                                        |
| **Binning / Bucketing**    | `pd.cut(df["age"],bins=[0,18,40,60])`                             | `CASE WHEN age<18 THEN 'Minor' ... END`                        | `SWITCH(TRUE(), age<18,"Minor", age<40,"Adult","Senior")`                  |
| **Index / Row Number**     | `df.reset_index()`                                                | `ROW_NUMBER() OVER(ORDER BY id)`                               | `RANKX(ALL(Table), Table[id])`                                             |

---
