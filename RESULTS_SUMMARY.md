## Exploring the effectiveness of simple top-down and bottom-up hierarchical time-series forecasting methods on the Walmart M5 dataset

In the realm of time-series forecasting, a collection of time series that follow a hierarchical aggregation structure often exists. This is known as hierarchical time series (HTS). The three common types of hierarchy are geographical, product and temporal. In some cases, the best HTS is a combination of these hierarchies. In essence, HTS can be beneficial for:
 - Borrowing "strength" from stronger datasets to poorer ones. 
 - Accounting for the unmeasured or unexplained variables.
 - Using the structure from the data collection step to interpret the data.

There are four common HTS methods that are currently understood. In order of simplicity, these are: 
- The top-down approach
- The bottom-up approach 
- The middle-out approach 
- The reconciliation approach 

In this work, we compare a direct ML model (using Random Forest classifier) with a simple weighted top-down and bottom-up approach. We start by defining a ML model at the top of the HTS chain and then compare the effectiveness of that model on lower levels with a simple weighted top-down and bottom-up approach. We assume four levels in our hierarchy, whereby:
- Level 1 = Total sales 
- Level 2 = Item categories
- Level 3 = Item sub-categories
- Level 4 = Granular items

![plot](/Users/user/hierarchical_time_series/HTS_chain.png)

 
Our direct ML model includes these features:
- wday = working day (1-7), where 1=Saturday and 7=Friday

- month = month of the year (1-12)

- event_type_1 = if there is an event (e.g. festive or national event), event_type_1 = 1

- week_of_year = the week of the year (1-52) 

- We also use exponential time smoothing of the target feature (sales) as an input feature. This is done later in the code. 

When we compare our ML model with a weighted top-down approach, our results showed that: 

- For level 2 to level 3 in the product hierarchy, we find that the top-down approach is better 2/3 times for FOODS items and 1/2 times for HOBBIES and HOUSEHOLD items. 

- For level 2 to level 4 in the product hierarchy, we find that the top-down approach is better 60-75% of the time for all items. 

- For level 3 to level 4 in the product hierarchy, we find that the top-down approach is better 60-75% of the time for all items. This is the same as what we have found for level 2 to level 4. 

When we compare our ML model with a weighted bottom-up approach, our results showed that: 

- For level 3 to level 2 of the hierarchy, we find that the bottom-up approach is better than direct modelling ~50% of the time. We show this for the FOODS category below. Note that the HOBBIES and HOUSEHOLD bottom up approaches were not as well-performing as the FOODS items.


Overall, we find that a simple weighted top-down or bottom-up approach can help simplify the problem is extremely high accuracy is not important. We also find that direct modelling of the granular items proves difficult due to the stochastic nature of the data and using a top-down approach can really help model these levels. In future, more advanced top-down and bottom-up approaches ought to be examined as the weighted approach is arguably too simplistic.

For further reading, please explore: 

https://medium.com/opex-analytics/hierarchical-time-series-101-734a3da15426

https://otexts.com/fpp2/gts.html