# Cohort Analysis
*To view the whole Jupyter Notebook and the code I used follow this link: [Cohort Analysis Notebook](https://nbviewer.org/github/laura-str/p100_Cohort_Analysis/blob/main/P100_Cohort_Analysis.ipynb)*

The task in this project was to help optimize marketing expenses of a company that promotes events & movies and sells tickets for them as well.

**The Datasets:**
* Server logs with data on visits from June 2017 through May 2018
* Dump file with all orders for the period
* Marketing expenses statistics

**The Tasks:**
* How do people use the product?
* When do they start to buy?
* How much money does each customer bring?
* When do customers pay off?


To answer these questions I had to sort users into cohorts, for example by the month they first visited or the time that passed between their first visit and their first purchase.

~~~~python
# defining a function that will add cohort name by conversion period
def cohort(row):
    
    conversion_days=row['conversion_days']
    
    if conversion_days == 0:
        cohort = '1: 0 days'
    elif  conversion_days <= 7:
        cohort = '2: 7 days'
    elif conversion_days <= 14:
        cohort = '3: 14 days'
    elif conversion_days <= 30:
        cohort = '4: 30 days'
    else:
        cohort = '5: > 30 days'
    return cohort

# applying the function to the orders table
orders['conversion_cohort'] = orders.apply(cohort, axis=1)
~~~~

### Conclusions
<img src="Cohort Analysis/Monthly_Visits.png">

* Most of our users use a desktop device to visit our website, the also spend more time on the website than touch device users
* The customers that already visited our website one year ago tend to visit the site more often and make more purchases
* Most users buy on their first visit or within the first week. After that they might return in later months for additional purchases
  
<img src="Cohort_Analysis.png">

* The cost of acquiring new customers is around USD 9.00, but we spend more in the last month.
* The average amount of money a customer spends during their lifetime is USD 10.00
* Most cohorts only reach their ROMI after 10 months
* Customers spend more per order when they come from sources #1 or #2 but the number of buyers that order on their first visit come from sources #3, #5 and #10
* Only two sources reached their ROMI, some others are close, but some like #3 are far from reaching it.
* We should concentrate our marketing efforts on sources that see early conversions, like #5 and #10 and sources that see the highest and fastest revenue like #1, #2 and #5.

source_id|revenue|costs|profit
---|--:|--:|--:
1|$45,298|$20,833|$24,465
2|$61,663|$42,806|$18,857
3|$43,146|$141,321|$-98,174
4|$48,308|$61,073|$-12,765
5|$45,248|$51,757|$-6,508
7|$1.22|-|-
9|$3,991|$5,517|$-1,525
10|$4,398|$5,822|$-1,424

We spend $77,000 more than we made, we need to cut back the marketing budget by at least this amount.

**Recommendations**

We should cut back the budget on source #3 where a lot of users converted early, and the number of buyers was the biggest, but they only spent $4.00 on average. We never came close to reaching ROMI from this source so maybe we should abandon this marketing channel altogether. Since we spend $141,321 on this source alone and only made $43,146 in return, abandoning this source would already gain us almost $100,000 which we could invest in more profitable sources.

[*See the whole Jupyter Notebook*](https://nbviewer.org/github/laura-str/p100_Cohort_Analysis/blob/main/P100_Cohort_Analysis.ipynb)

