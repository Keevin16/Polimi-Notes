### ⭐ [[Star schema]]
>The Data Warehouse Model it's based on the [[Star schema]]

![[Pasted image 20250419122339.png]]
It's a representation of multi - perspective analysis
At the **center** of the **star** there's the important concept (**concept of interest**, called "**[[FACT]]**") and each **spike** is one **perspective** analysis.
The **FACT** has 1 to 1 cardinality with each spike and primary key to access to each table.
![[Pasted image 20250419123121.png]]

---
### ❄️ Snowflake Schema
>It's the evolution of the star schema, is more complex than the Star one
>In this case each spike becomes a **multi-spike**, every **dimension** can be split in **sub-dimensions**, and sub-dimensions can be split in **sub-sub-dimensions** and so on.

![[Pasted image 20250419123706.png]]
Cardinalities are always (1,1) and (0,N)
- From the **center** to the **outside** the **flow is unique** 
	for a given sale there is only one store, for a given store there is only one city
- From the **outside** to the **center** the **flow is not unique**
	for a given country there could be multiple regions

Remark:
	The farther you move from the center, the larger the dataset becomes

**OPERATIONS** that is possible to do in this schema:
[[Drill-down]]🔽
Means going from less detailed to more detailed data --> Add one analysis dimension (**dis aggregation**)
	e.g. : Zoom in google maps or from **Year → Quarter → Month → Day**.

[[Roll-up]]🔼
Instead in this case going from **more detailed** to **less detailed** data -->Remove one analysis dimension (**aggregation**)
	e.g.: From daily sales → monthly total → quarterly total → annual total.

---
[[Data cube]]
It's a **multidimensional array of data**, each **dimension** (equal to the dimension on the [[Star schema]]) represents a different **attribute**, and each **cell** contains a **measure**.
![[Pasted image 20250419152225.png]]
#### [[Slice and Dice]]
**Slice** **fixes a single value in one dimension** → returns a **2D sub-cube**.
	like sales for a specific region
![[Pasted image 20250419152514.png]]

**Dice** **selects specific values from multiple dimensions** → returns a **smaller sub-cube**.
	Dice where Product ∈ {Laptop, Phone}, Region = 'Europe', Time ∈ {2023, 2024}
![[Pasted image 20250419152637.png]]

#DataWarehouse