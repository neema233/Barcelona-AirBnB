# AirBnB Data Modeling Project ✈️🏡
# Project Overview :
This document outlines the business need for data modeling of Airbnb listings data for Barcelona, focusing on extracting insights to improve user experience and enhance decision-making for both hosts and guests.

Tools used: Excel,Power BI

**Specific business requirements that needs to cover in modeling:** 

*1. Identify cost-effective options:*

Determine the cheapest listing with the highest availability in a specific month (January 2024). This helps budget-conscious travelers find the most affordable accommodations.

*2. Highlight popular listings:*

Identify listings with the most reviews in a particular month (November 2023). This aids travelers in discovering highly rated and potentially desirable options based on past guest experiences.

*3. Analyze neighborhood trends:*

Determine the neighbourhood with the highest average listing price. 

*4. Provide personalized recommendations:*

Develop a system to recommend listings based on user-specified criteria. This includes:

. A family vacation scenario for a man, wife, and 2 children seeking a week-long stay around March 2024 (accommodating capacity and family-friendly amenities).

. A group of college students (5 people) seeking a budget-friendly option for New Year's Eve celebrations, including two additional days before and/or after (consider capacity, affordability, and proximity to festive events).
# *Data Resource:*
[insideairbnb.com](insideairbnb.com)
# *Data Profiling* 
Table names and descriptions:

***Listings Table :***

```id``` Unique identifier for each listing

```listing_url:``` URL of the listing on Airbnb

```scrape_id:``` Identifier for when the data was scraped.

```last_scraped:``` Date the data was last scraped.

```source:``` the source of data which is airBnB website.

```name,description:``` Name of the property and its description

```neighborhood_overview:``` Description of the neighborhood

```picture_url:``` URL of the main image for the view of apartment.

```host_id:``` Unique identifier for the host.

```host_url:``` Host's profile page on Airbnb.

```host_name:``` Host's name.

```host_since:``` Year the host joined Airbnb.

```host_location:``` Host's listed location.

```host_about:``` Description provided by the host.

```host_response_time:``` Typical response time to inquiries.

```host_response_rate:``` Percentage of inquires response.

```host_acceptance_rate:``` Percentage of booking requests accepted.

```host_is_superhost:``` Flag for if host has superhost status.

```Various host profile photo URLs```: url are diffrent in the size of the picture.

```host_neighbourhood:``` Neighborhood the host lists.

```Various counts of host's listings:``` host_listings_count,host_total_listings_count
Example:A host with host_listings_count = 2 and host_total_listings_count = 5 might have 2 listings currently available and have previously offered 3 others that are now inactive.

```host_verifications:``` What verification the host has completed

```host_has_profile_pic:``` Flag for profile photo

```host_identity_verified:``` Flag if identity is verified

```Neighborhood data``` like name, latitude, longitude

```Property details``` like type, room type, capacity, bathroomsAmenities included

```Pricing details``` like nightly rate, minimum stays

```Some Calendar info``` like availability for 30 to 365 next days, last calendar scrape

```Review details``` like count, scores

```license:``` Listing license

```instant_bookable:``` Instant bookable status

Various calculated host listing counts

Reviews per month

***Reviews Table :***

```listing_id:``` identifier for each listing.

```id:``` review id.

```date:``` date of the review.

```reviewer_id:``` identifier of each reviewer.

```reviewer_name:``` the name of the reviewer.

```comments:``` the review text.

***calendar table:***

```listing_id:``` identifier for each listing.

```date: ``` the date of listings calender

```available:``` Flag indicating whether the listing is available on that date.

```price:```  price of the listing for that date.

```adjusted_price:``` Price after considering any discounts or promotions applied to the base price(it was empty in our case)

```minimum_nights:``` Minimum number of nights a guest can book the listing for that date (null if no minimum).

```maximum_nights:``` Maximum number of nights a guest can book the listing for that date (null if no maxmuim).

***neighbourhood table:***

there are two columns ```neighbourhood_groups``` and ```neighbourhood``` 

# *Model Explanation:*
***Fact Table***

Listings Facts:
```listings_id```,  ```PropertyID(FK)```, ```neighbourhood_id(FK)```, ```host_id(FK)```,```listing_url```, ```scrape_id```, ```last_scraped```,```lastscraped_datekey(FK)```, ```source```, ```picture_url```, ```host_response_time```, ```host_response_rate```, ```host_acceptance_rate```, ```accommodates```, ```bathrooms```, ```beds```, ```price```, ```minimum_nights```, ```maximum_nights```, ```minimum_minimum_nights```, ```maximum_minimum_nights```, ```minimum_maximum_nights```, ```maximum_maximum_nights```, ```minimum_nights_avg_ntm```, ```maximum_nights_avg_ntm```, ```calendar_updated```, ```has_availability```, ```availability_30```, ```availability_60```, ```availability_90```, ```availability_365```, ```calendar_last_scraped```,```calender_last_scraped_datekey(FK)```, ```number_of_reviews```, ```number_of_reviews_ltm```, ```number_of_reviews_l30d```, ```first_review```,```first_review_datekey(FK)```, ```last_review```,```last_review_datekey(FK)```, ```review_scores_rating```, ```review_scores_accuracy```, ```review_scores_cleanliness```, ```review_scores_checkin```, ```review_scores_communication```, ```review_scores_location```, ```review_scores_value```, ```license```, ```instant_bookable```, ```calculated_host_listings_count```, ```calculated_host_listings_count_entire_homes```, ```calculated_host_listings_count_private_rooms```, ```calculated_host_listings_count_shared_rooms```, ```reviews_per_month```

***Dimension Table***

1. Date DIM (Role playing DIM)

   it consists of ```DateKey(PK)```,```Date```,```year```,```month```,```day```,```Quarter```,```dayOfWeek```,```MonthOfYear```
   
2. Prpoerty DIM
   
   it represent the type of apartment,room and bathroom
   
   it consists of ```propertyID```,```description```,```property_type```,```room_type```,```bathrooms_type```
   
3. Host DIM
   
   it represent the information about the host
   
   it consists of ```host_id```, ```host_url```, ```host_name```, ```host_since```, ```host_location```, ```host_about```, ```host_response_time```, ```host_response_rate```, ```host_acceptance_rate```, ```host_is_superhost```, ```host_thumbnail_url```, ```host_picture_url```, ```host_neighbourhood```, ```host_verifications```, ```host_has_profile_pic```, ```host_identity_verified```

4. Neighbourhood DIM
   
   it reprsent information about neighbourhood
   
   it consists of ```neighbourhood_ID```, ```neighbourhood```, ```neighbourhood_group```, ```neighbourhood_cleansed```, ```latitude```, ```longitude```, ```neighborhood_overview```

5. Review DIM
   
   it reprsent information about review
   
   it consists of ```review_id```, ```listing_id```,```reviewer_id```, ```reviewer_name```, ```comments```

6. Calender DIM

   it consists of ```calender_datekey```, ```listing_id```, ```calender_date```, ```available```, ```price```, ```minimum_nights```, ```maximum_nights```

***Modeling***
![Data Modeling](https://drive.google.com/file/d/1vWTlETPhYhgapJ4q3lJpkj9GkMOiutPc/view?usp=drive_link)


