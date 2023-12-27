# 📊 Sharing Insights: Optimizing Shipments and Profitability 

The main focus revolved around improving customer service, increasing sales, and reducing operational costs. Let me provide you with a quick summary of the insights shared on my 3-page dashboard:
***
## 1️⃣ Executive Summary:

Identified the top-performing products.
Analyzed profit percentages for strategic decision-making.
Objective: Drive sales and optimize profitability.
***
## 2️⃣ Shipping Metrics:

Explored the correlation between shipping quantity and cost.
What-if analysis revealed that single quantity shipping is costlier, while bulk shipments reduce per-unit costs.
Goal: Optimize shipping costs for efficiency.
***
## 3️⃣ Market Basket Analysis:

Recognized patterns in customer purchasing behavior.
Identified potential cross-selling opportunities.
Objective: Enhance revenue through optimized market baskets.
***
### 🎨 Design Approach:

Prioritized alignment for clarity.
Utilized white spaces for a clean and appealing aesthetic.
Employed a thoughtfully chosen color palette for visual cohesion.
***
## 🎯 Mission: Serve More, Sell More, Spend Less! 
***

## 🗝️ Some Key DAX Formulas


### Blended Shipping Cost Factor

````sql
Blended Shipping Cost Factor =
    IF('What-if quantity'[What-if quantity Value]<=1,1,
    IF('What-if quantity'[What-if quantity Value]<=2,0.8,
    IF('What-if quantity'[What-if quantity Value]<=4,0.6,
    IF('What-if quantity'[What-if quantity Value]<=7,0.5,
    IF('What-if quantity'[What-if quantity Value]<=9,0.4,0.3)))))
````
***

### Shipping(What-if)
````sql
Shipping(What-if) = 
SUMX(Sales, 
     IF(Sales[Quantity]=1,
        Sales[Shipping Cost],
        Sales[Shipping Cost]+(((Sales[Quantity])-1)*
        (Sales[Shipping Cost]*[Blended Shipping Cost Factor]))))
````
***
### Baseline running total
````sql
Baseline running total = 
SUMX(FILTER(ALLSELECTED(Sales), Sales[Transaction Date]
    <=MAX('Market Basket'[Transaction Date])), [Shipping (Baseline)])
````

***
### What-if running total
````sql
What-if running total = 
SUMX(FILTER(ALLSELECTED(Sales), Sales[Transaction Date] 
    <=MAX('Market Basket'[Transaction Date])), [Shipping(What-if)])
````

***
### Shipping (Baseline)
````sql
Shipping (Baseline) = 
SUMX(Sales,IF(Sales[Quantity]=1,Sales[Shipping Cost],Sales[Shipping Cost]
             +(((Sales[Quantity])-1)*(Sales[Shipping Cost]*0.7))))

````
***
[**Download .pbix File**](https://github.com/alezirczy/Power-Bi-Projects/blob/main/%231%20Logistic%3A%20Optimizing%20Shipments%20and%20Profitability/Logistics%20Operation%20-%20Optimizing%20Shipments%20and%20Profitability%20v2.pbix)

***


<h2 align="center">Report (1st Page)</h2>


<img src="https://github.com/alezirczy/Images/blob/main/%231%20Optimizing%20Shipments%20and%20Profitability/Executive%20Summary%20-%20Report%20(1st%20Page).png">

***
<h2 align="center">Report (2nd Page)</h2>
<img src="https://github.com/alezirczy/Images/blob/main/%231%20Optimizing%20Shipments%20and%20Profitability/Shipping%20Metrics%20-%20Report%20(2nd%20Page).png">


***
<h2 align="center">Report (3rd Page)</h2>
<img src="https://github.com/alezirczy/Images/blob/main/%231%20Optimizing%20Shipments%20and%20Profitability/Market%20Basket%20-%20Report%20(3rd%20Page).png">

