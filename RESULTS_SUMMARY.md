# Hierarchical Time Series with Walmart M5 dataset

Time series forecasting is a common Data Science task and is used in many applications including demand forecasting, stock-market returns and in predictive maintenance. Often times, real-world time series follow a hierarchical aggregation structure which arise from typical hierarchies like:

* geographical (e.g. COVID cases broken down by regions - https://coronavirus.data.gov.uk/details/interactive-map),
* product (e.g. supermarket product categories in Walmart M5 dataset),
* temporal (e.g. website visitors by day, week, month).

In practice, hierarchical time series (HTS) are often treated individually without taking into account their hierarchical nature. However, exploiting the hierarchical nature using HTS methods can be beneficial for:

1. Borrowing "strength" from stronger datasets to poorer ones.
2. Accounting for the unmeasured or unexplained variables.
3. Using the structure from the data collection step to interpret the data.

There are four common HTS methods that are currently understood. In order of simplicity, these are (1 being the simplest):

1. The top-down approach
2. The bottom-up approach
3. The middle-out approach
4. The reconciliation approach

In this work, we compare a direct ML model (using Random Forest regressor) with a simple weighted top-down and bottom-up approach. We start by defining a ML model at the top of the HTS chain and then compare the effectiveness of that model on lower levels with a simple weighted top-down and bottom-up approach. We assume four levels in our hierarchy, whereby:

* Level 1 = Total sales
* Level 2 = Item categories
* Level 3 = Item sub-categories
* Level 4 = Granular items

![alt text](https://github.com/EdrisKhorani/hierarchical_time_series/blob/master/HTS_chain.png)

Our direct ML model includes these features:

* 'wday' = working day (1-7), where 1=Saturday and 7=Friday
* 'month' = month of the year (1-12)
* 'event_type_1' = if there is an event (e.g. festive or national event), event_type_1 = 1
* 'week_of_year' = the week of the year (1-52) 
* We also use exponential time smoothing of the target feature (sales) as an input feature. 

When we compare our ML model with a weighted top-down approach, our results showed that:

* For level 2 to level 3 in the product hierarchy, we find that the top-down approach is better ~66% times for FOODS items and ~50% times for HOBBIES and HOUSEHOLD items.
* For level 2 to level 4 in the product hierarchy, we find that the top-down approach is better 60-75% of the time for all items.
* For level 3 to level 4 in the product hierarchy, we find that the top-down approach is better 60-75% of the time for all items. This is the same as what we have found for level 2 to level 4.

When we compare our ML model with a weighted bottom-up approach, our results showed that:

* For level 3 to level 2 of the hierarchy, we find that the bottom-up approach is better than direct modelling ~50% of the time. We show this for the FOODS category below. Note that the HOBBIES and HOUSEHOLD bottom up approaches were not as well-performing as the FOODS items.

Overall, we find that a simple weighted top-down or bottom-up approach can help simplify the problem if achieving extremely high accuracy is not a top priority. We also find that direct modelling of the granular items proves difficult due to the stochastic nature of the data and using a top-down approach can really help model these levels. In future, more advanced top-down and bottom-up approaches ought to be examined as the weighted approach is arguably too simplistic.

For further reading, please explore:

[Hierarchical Time Series 101] https://medium.com/opex-analytics/hierarchical-time-series-101-734a3da15426

[Forecasting: Principles and Practice - 10.2 Grouped time series] https://otexts.com/fpp2/gts.html
