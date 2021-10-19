# Portfolio
### *This is a repository to showcase projects I worked on.*

## [Cohort Analysis](Cohort%20Analysis)

In this project I did a cohort analysis, calculating retention rates, ROMI, LTV and CAC.

<img src="Cohort Analysis/Cohort_Analysis.png">

The language I used for this is **Python**, some libraries I used are *pandas*, *matplotlib* and *seaborn*.

I recommend viewing the notebook directly on nbviewer to make sure that it is rendered correctly, and the hyperlinks work:

[**See the Project**](Cohort%20Analysis)

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
orders['conversion_cohort'] = orders.apply(cohort,axis=1)
~~~~