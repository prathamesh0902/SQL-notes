# 📊 Data Transformation Cheat Sheet (Python | SQL | DAX)

---

## 🔹 Common Data Transformations

| Transformation    | Python (Pandas)                                      | SQL                                             | DAX (Calculated Table / Measure)          |
| ----------------- | ---------------------------------------------------- | ----------------------------------------------- | ----------------------------------------- |
| Filter & Sort     | `df[df['age'] > 20].sort_values('name')`             | `SELECT * FROM t WHERE age > 20 ORDER BY name;` | `FILTER(Table, Table[age] > 20)`          |
| Pivot             | `df.pivot(index='id', columns='attr', values='val')` | `PIVOT (SUM(val) FOR attr IN ('A','B'))`        | `SUMMARIZECOLUMNS([id], "A", [MeasureA])` |
| Merge (Join)      | `pd.merge(df1, df2, on='id', how='left')`            | `SELECT * FROM t1 LEFT JOIN t2 ON t1.id=t2.id;` | `LOOKUPVALUE()` / `RELATED()`             |
| Append (Union)    | `pd.concat([df1, df2])`                              | `SELECT * FROM t1 UNION ALL SELECT * FROM t2;`  | `UNION(Table1, Table2)`                   |
| Replace Values    | `df['col'].replace('old','new')`                     | `REPLACE(col,'old','new')`                      | `SUBSTITUTE([col],"old","new")`           |
| Remove Duplicates | `df.drop_duplicates()`                               | `SELECT DISTINCT * FROM t;`                     | `DISTINCT(Table)`                         |

---

## 🔹 Data Cleaning & Standardization

| Transformation | Python (Pandas)                  | SQL                                         | DAX                                         |
| -------------- | -------------------------------- | ------------------------------------------- | ------------------------------------------- |
| Trim Text      | `df['col'].str.strip()`          | `TRIM(col)`                                 | `TRIM([col])`                               |
| Case Change    | `df['col'].str.upper()`          | `UPPER(col)`                                | `UPPER([col])`                              |
| Handle Nulls   | `df['col'].fillna(0)`            | `COALESCE(col,0)`                           | `IF(ISBLANK([col]),0,[col])`                |
| Type Cast      | `df['col'].astype(int)`          | `CAST(col AS INT)`                          | `CONVERT([col], INTEGER)`                   |
| Group By       | `df.groupby('cat')['val'].sum()` | `SELECT cat, SUM(val) FROM t GROUP BY cat;` | `SUMMARIZE(Table,[cat],"Total",SUM([val]))` |

---

## 🔹 Advanced Transformations

| Transformation     | Python (Pandas)                    | SQL                                        | DAX                                |
| ------------------ | ---------------------------------- | ------------------------------------------ | ---------------------------------- |
| Rank               | `df['rank']=df['val'].rank()`      | `RANK() OVER(ORDER BY val DESC)`           | `RANKX(ALL(Table),[Measure])`      |
| Conditional Column | `np.where(df['v']>5,'High','Low')` | `CASE WHEN v>5 THEN 'High' ELSE 'Low' END` | `IF([v]>5,"High","Low")`           |
| Top N              | `df.nlargest(10,'val')`            | `ORDER BY val DESC LIMIT 10`               | `TOPN(10,Table,[val],DESC)`        |
| Index Column       | `df.reset_index()`                 | `ROW_NUMBER() OVER(ORDER BY id)`           | `RANKX(ALL(Table),[ID],,ASC)`      |
| Running Total      | `df['val'].cumsum()`               | `SUM(val) OVER(ORDER BY date)`             | `TOTALYTD([Measure],'Date'[Date])` |

---

## 🔹 Specialized Transformations

| Transformation | Python (Pandas)                    | SQL                          | DAX                                |
| -------------- | ---------------------------------- | ---------------------------- | ---------------------------------- |
| Date Part      | `df['date'].dt.year`               | `EXTRACT(YEAR FROM date)`    | `YEAR([Date])`                     |
| Text Split     | `df['col'].str.split('-').str[0]`  | `SPLIT_PART(col,'-',1)`      | `LEFT([col], SEARCH("-",[col])-1)` |
| Binning        | `pd.cut(df['val'],bins=[0,10,20])` | `WIDTH_BUCKET(val,0,100,10)` | `FLOOR([val],10)`                  |

---

