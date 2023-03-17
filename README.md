# Airbnb Listing Price Prediction

## Project objective

New York is one of the most important markets for Airbnb, with the number of available short-term rentals has eclipsed that of long-term rentals in this May, according to a comparison of reports from Douglas Elliman and Airbnb number-crunching websites . And the news comes at a time when rental housing inventory is at a serious crunch with record-high prices in the wake of COVID-19 and bidding wars for available units driving prices higher. However, a too-high pricing would not lead to a lasting high satisfaction of customer, so it would not be an optimal price; while a too-low pricing would neither be a good choice as it will lead to lower revenue. 

By “learning” the “well-priced” listing data in machine, I am aiming to predict optimal prices dynamically and provide suggestions to hosts for their new listings.

## Datasets

We obtain the data source from Inside Airbnb , the original dataset includes 37, 631 listings with 74 features summarized below:
- Location related:  longitude, latitude, neighbourhood
- Property related: property type, room type, accommodates, bedrooms, beds, bathroom, description, amenities
- Booking related: availability 30d/60d/90d/365d, instant bookable, minimum_nights, maximum_nights
- Review related: number of reviews, number_of_reviews_ltm/l30d, first/last review date, review scores, reviews_per_month
- Host related:  host_response_time, host_acceptance_rate, host since date, super_host, host_listings_count

## Feature Engineering and Pre-processing 

- Using external coordinate data to calculate the distance (haversine distance) from subway stations, shopping centres, and 10 popular tourist destinations (such as The Empire State Building, Statue of Liberty…) based on listings' coordinates found in the original Airbnb dataset. 
- Listing description was processed into numerical values such as word counts to explore any correlation between how the listings are described and the price they can command. 
- Features that are generally perceived to be important - bathrooms, and host response/acceptance rates – and that were stored as text variations were transformed to float. 
- I made the decision to convert listings’ coordinates to actual distances from amenities to ensure the model results are easily explainable, as it is much easier to understand listing location advantages if pecked to specific landmarks, at the expense of more granularity provided by the coordinates. 
- Removing the redundant or repeated columns (total 39 columns) and numeric features that were found to have a high correlation.

## Models

- Linear Regression (with L1,L2 regularizations)
- Decision Tree
- Random Forests
- Extra Tree
- Gradient Boost
- XGB
- Stacking Regressor

Metrics: R-squared

## Results

The stacking model achieved a R-squared of 0.68 and 0.67 on the train and test dataset, respectively.

## Future Works

- My suggestion to improve the R-squared score is to incorporate the latitude and longitude as features. The currently-used approach prioritized interpretability hence the latitude and longitude data were transformed into distance information between listings and areas of interest such as subways and attractions. 
- The dataset used for this project only covers a snapshot in time, and therefore the predicted price is only applicable for the same period. An extension of this project is to consider using a dataset with time-based pricing data to account for the fluctuation of prices over time. This can improve the application of the model to cover other time periods in the year as it can consider seasonal trends. 
- The model can be expanded to consider other cities or areas. The original dataset is only for New York City, and Airbnb is present in over 100,000 cities. With more cities, an extension would be to understand if feature importance varies per city or location. 


