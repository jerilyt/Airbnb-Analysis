---
title: Exploring for Airbnb Dataset in Germany - Data Cleaning Challenge
date: 2020-08-04 20:18:33
tags:
- Airbnb Listings
- Exploratory Analysis
- Data Cleaning
- Feature Engineering
categories:
- Machine Learning
---

Even though these short term rentals may no longer be booked for vacation or leisure purposes because of coronavirus crackdown recently, we can not deny that Airbnb has seen a meteoric growth since its inception in 2008 with the number of rentals listed on its website growting exponentially every year. I wish this bussiness may flourish again one day, because it definitely makes a cozy place for living or travelling. In the past 

I will be working with Prenzlauer Berg data, one neighborhood of Berlin. Located in the district of Pankow, Prenzlauer Berg is one of the most charismatic neighborhoods there, with countless of bars and cafes. For many reasons, Prenzlauer Berg is a common choice as a base for the visitors of Berlin. There are different varieties of Airbnb properties in this area, so let us driven into it!

<!--more-->

Acturally, this project is done in R three months ago, including data preparation & exploration, rental price prediction, clustering analysis to place rentals. I will write three blogs to illustrate my project here. 

In this blog, I will perform an exploration anlysis at first. The Airbnb dataset is sourced from [**Inside Airbnb**](http://insideairbnb.com/get-the-data.html) website, including detailed listings data. 

**A quick glance at the data shows that there are:**

- 3899 unique listing in Prenzlauer Berg in total. And the first rental was up in August, 2008 by a host from Florida. 
- Rental price is ranging from 0 dollar to 5000 dollars for one night. Listing with \$ 5000 price tag, a hostel with a little infomation about host and hostel, may be one outlier in dataset. 

In my oppinion, Data Cleaning is the most fundamental but essential work in data analysis. Not only because incorrect data can reduce the modeling effectiveness, but also because we can explore more deeper into this dataset. They exist side by side and play a part together. Without that understanding, we have no basis from which to make decisions about what data is relevant as we clean and prepare our data.

Data cleaning is the process of cleaning or standardising the data to make it ready for analysis. Most of times, we deal with discrepancies such as incorrect data formats, missing data, errors. It is irrational to delete data with missing values because they may reveal some information. Besides the type errors, there are still many reasons to make it. The Airbnb dataset is . It's an interesting challenge. In this blog, I will illustrate how I cope with them.

## Handling missing values

See how many missing data points we have

In the raw dataset, there are too many missing values in the form of entire rows with all NA value. We just delete them because there is no meaning. After we delete 1131 NA rows, let's see how many we have in each column.

| Feature                          | Number of NA | How it looks like                                            |
| -------------------------------- | ------------ | ------------------------------------------------------------ |
| square_feet                      | 2695         | NA 720 NA NA NA NA NA NA NA 1012                             |
| license                          | 2564         | <NA> 03/Z/RA/003410-18 <NA>                                  |
| monthly_price                    | 2392         | "\$1,000.00", "​\$1,001.00", NA                               |
| weekly_price                     | 2253         | "\$1,000.00","$1,050.00",NA                                  |
| notes                            | 1894         | " I have a cat, please be aware if you have an allergy.", NA |
| interaction                      | 1530         | " feel free to contact me or my person of trust any time",NA |
| host_response_time               | 1502         | "a few days or more", "within a week", NA                    |
| host_response_rate               | 1502         | "0%,"10%","100%", NA                                         |
| access                           | 1462         | " Available inside the room there will be a kettle …", NA    |
| neighborhood_overview            | 1335         | " A mix of Celebrities the Young Creative Scene…", NA        |
| house_rules                      | 1313         | "_ keine laute Musik _ bitte nicht mit…" ,NA                 |
| host_about                       | 1271         | "We love to travel ourselves a lot and prefer to stay in  apartments…" NA |
| transit                          | 1152         | "The apartment is situated 3min on foot from the Station Hermannstr.  ",NA |
| security_deposit                 | 1064         | "$0.00","$1,000.00", NA                                      |
| cleaning_fee                     | 768          | "$0.00","$10.00",NA                                          |
| host_neighbourhood               | 606          | "Adlershof","Alt-Hohenschönhausen",NA                        |
| review_scores_value              | 505          | NA 9 9 10 9 10 9 10 NA 9                                     |
| review_scores_checkin            | 505          | NA 9 10 10 9 10 9 10 NA 9                                    |
| review_scores_location           | 504          | NA 10 10 10 9 10 10 10 NA 10                                 |
| review_scores_communication      | 502          | NA 9 10 10 10 10 8 9 NA 9                                    |
| review_scores_accuracy           | 502          | NA 9 10 10 10 10 9 10 NA 9                                   |
| review_scores_cleanliness        | 501          | NA 9 10 10 10 10 9 10 NA 9                                   |
| review_scores_rating             | 500          | NA 92 96 100 93 96 87 94 NA 91                               |
| reviews_per_month                | 445          | NA 1.25 1.75 0.15 0.23 2.83 0.75 0.18                        |
| first_review                     | 445          | 2009-06-20,"2009-08-18",NA                                   |
| last_review                      | 444          | 2010-09-16,"2011-01-26",NA                                   |
| summary                          | 130          | "Ich bin sehr stolz darauf meine Wohnung freundlichen  Berlinbesuchern", NA |
| zipcode                          | 83           | 10115,"10115\n10115",NA                                      |
| state                            | 19           | "berlin","Berlin",NA                                         |
| description                      | 16           | " 24m2 room in Neukoelln with large double bed, …" NA        |
| host_location                    | 11           | "Berlin, Berlin, Germany ","Coledale, New South Wales,  Australia", NA |
| market                           | 9            | Berlin,"Juarez",NA                                           |
| name                             | 8            | "\tThe right place for your  stay", NA                       |
| bathrooms                        | 7            | NA 1.0 1.0 2.5 1.0 1.0                                       |
| beds                             | 2            | NA 2 2   7 1 1                                               |
| host_total_listings_count        | 1            | NA 1 1   1 3 1                                               |
| host_since                       | 1            | "2008-10-19", "2009-05-16",  "2009-08-25","2009-11-18", NA   |
| host_name                        | 1            | "Britta","Bright","Philipp", " Chris +  Oliver", "Wolfram",NA |
| host_listings_count              | 1            | NA 1 1 1 3 1 1 2 NA 2 …                                      |
| host_is_superhost                | 1            | "f","t", NA                                                  |
| host_identity_verified           | 1            | "f","t", NA                                                  |
| host_has_profile_pic             | 1            | "f","t", NA                                                  |
| city                             | 1            | Berlin Berlin Berlin Berlin Berlin  NA                       |
| bedrooms                         | 1            | 1 1 4 0 1 2 2 2 0 2                                          |
| street                           | 0            | "\nKreuzberg, Berlin, Germany"…                              |
| smart_location                   | 0            | "\nKreuzberg, Germany"…                                      |
| room_type                        | 0            | Entire home/apt  Private  room   Shared room                 |
| requires_license                 | 0            | f  t                                                         |
| require_guest_profile_picture    | 0            | f  t                                                         |
| require_guest_phone_verification | 0            | f  t                                                         |
| property_type                    | 0            | Apartment  Apartment  Apartment   Apartment  Condominium …   |
| price                            | 0            | $0.00,"$1,000.00"                                            |
| number_of_reviews                | 0            | 143 197 6 23 279 56 18 163 28 69                             |
| neighbourhood_group_cleansed     | 0            | Charlottenburg-Wilm.,…                                       |
| neighbourhood_cleansed           | 0            | Adlershof,"Albrechtstr."…                                    |
| neighbourhood                    | 0            | Adlershof,"Alt-Hohenschönhausen" …                           |
| minimum_nights                   | 0            | 62 2 6 90 3 3 3 3 90 60                                      |
| maximum_nights                   | 0            | 1125 10 14 1125 30 30 21 1125 1125 365                       |
| longitude                        | 0            | 13.4 13.4 13.4 13.4 13.4                                     |
| latitude                         | 0            | 52.5 52.5 52.5 52.5 52.5                                     |
| last_scraped                     | 0            | 2018-11-07 2018-11-09                                        |
| is_location_exact                | 0            | "f","t"                                                      |
| is_business_travel_ready         | 0            | "f","t"                                                      |
| instant_bookable                 | 0            | "f","t"                                                      |
| id                               | 0            | 3176 7071 9991 14325 17409 20858 24569                       |
| host_verifications               | 0            | "['email', 'facebook', 'jumio', 'offline_government_id',  'government_id']"… |
| host_id                          | 0            | 3718 17391 33852 55531 67590                                 |
| has_availability                 | 0            | "t"                                                          |
| guests_included                  | 0            | 2 1 5 1 1 2 2 4 1 2                                          |
| extra_people                     | 0            | $0.00","$10.00",…                                            |
| country_code                     | 0            | "DE"                                                         |
| country                          | 0            | "Germany"                                                    |
| cancellation_policy              | 0            | "flexible","moderate",..                                     |
| calendar_updated                 | 0            | " 1 week ago", "10 months ago", "11 months  ago", "12 months ago"... |
| calendar_last_scraped            | 0            | "2018-11-07","2018-11-09"                                    |
| calculated_host_listings_count   | 0            | 1  2  3    4  5  6    7  8  9   10  11  12   13  15  16   19  45 |
| bed_type                         | 0            | Airbed     Couch     Futon Pull-out Sofa   Real Bed          |
| availability_90                  | 0            | 0  1    2  3  4    5  6  7    8  9  10   11  12  13   14  15  16 |
| availability_60                  | 0            | 0  1    2  3  4    5  6  7    8  9  10   11  12  13   14  15  16 |
| availability_365                 | 0            | 0  1    2  3  4    5  6  7    8  9  10   11  12  13   14  15  16 |
| availability_30                  | 0            | 0  1    2  3  4    5  6  7    8  9  10   11  12  13   14  15  16 |
| amenities                        | 0            | {Internet,Wifi,Kitchen,"Buzzer/wireless intercom",Crib}...   |
| accommodates                     | 0            | 1  2    3  4  5    6  7  8    9  10  11   12  16             |

 That seems like a lot! For almost cells in this dataset are empty. In the next step, we are going to take a closer look at some of the columns with missing values and try to fighure out what might be going on with them,

### Figure out why the data is missing

This is the point at which we get into the part of data science that I like to call "data intution", by which I mean "really looking at your data and trying to figure out why it is the way it is and how that will affect your analysis". It can be a frustrating part of data science, especially if you're newer to the field and don't have a lot of experience. For dealing with missing values, you'll need to use your intution to figure out why the value is missing. One of the most important question you can ask yourself to help figure this out is this:

Before we impute the missing value, it is a critical point to get into this part. This helps us to get "data intuition" by really looking at your dataset and trying to figure out why it is this way and how that will affect your analysis. Keep the feature or not is a really important question for analysis, and you can ask yourself **"Is this value missing becuase it wasn't recorded or becuase it dosen't exist?"** 

For the first thing, like square_feet of house is existed but some hosts do not input this kind of data for many possible reasons, we should consider to impute them in a proper way or delete them directly. These value you probaly do not want to keep them as NA. Also, you can try to guess what it might have been based on the other values in that column and row. However, if the value is missing because it doesn't exist, for example monthly_price and weekly_price for some listings, we should consider feature engineering to transform them into more meaningful features. Some listings do not have monthly prices or weekly price because they do not offer the discounts for long-term renting. It tells us a lot! Something like "probably the host want to make profit by offering discount because his/her house is more suitable for  long-term accommodation. Maybe no visitor who traveling here wants to live in this place. Or the host think only rent for one day can not get profit, and he/she have to clean or manage this accommodation everyday. In this way, I made new features about how many discounts that the house provide. (I will talk it in the latter content.)



### Ways to handle missing values

Let me talk about the way to handle missing values in many situations. 

* **Drop Columns with Missing Values**

Even though square_feet is an significant variable toward rent price, there are too many missing value here. inproper imputation may bring more bias. Let take mean imputation for an example. If we impute missing value as mean value, and regard it is missing randomly, then the mean estimator is unbiased. This is the logic to achieve the mean i putation. However, if we do in this way, we do not keep the relationships with other variables. Statistically, the estimator is unbiased, but the standard deviation is biased. And most of our interest is to find the relationships, so mean imputation is not a good choice.  In this case, we can not use simple option to fill square_feet with the null value. Also, we can not find any straight relationships with this variable.  Take many factors into consideration, we just drop this column directly. 



* **Feature Engineering**

  * Whether or not

  license is a feature discribe the host's license. If host has that, they should upload the exact license code here. Acturally, we don't care about the exact text information on that. Whether has license or not is more meaningful for us. Therefore, I transform the license code as "T", and missing value as "F". "T" is the abbreviation of "true", representing the host has license code for the accomendation. While "F" is "false", which means they do have license code. 

  ```R
  PB_3$license[which(is.na(PB_3$license)==F)] = "Yes"
  PB_3$license[which(is.na(PB_3$license)==T)] = "No"
  ```

  The dataset still has some variables which can handle in the same method.

  * Date to Time 

  First review date is an important feature for analysis. It tells us how long does the host operating this accomendation. However, as a category variable, first_review will be re-encoded as many 0/1 variables. We can transform the date as days, a numeric variable. How to transform? Create a new feature.

  Here, I created a new feature Business_interval, which measures number of day after this airbnb has first review. Also, same method works on other date variables, like last_review, host_since. I created a feature named No_Business_interval. This measures number of day after the last review. Longer interval means this airbnb is no business recently. And the third feature is operation_interval, which is number of day after host_since. This measure how long that the airbnb is. 

  There are missing value in first_review and last_review the two variables. The reason would be there is no review. Therefore, the time interval would be 0.

  ``` R
  first_review = as.Date(PB_2$first_review,"%Y-%m-%d")
  last_review = as.Date(PB_2$last_review,"%Y-%m-%d")
  host_since = as.Date(PB_2$host_since,"%Y-%m-%d")
  Business_interval = today() - first_review
  No_Business_interval = today() - last_review
  operation_interval = today() - host_since
  
  Business_interval[is.na(Business_interval) == T] = 0
  No_Business_interval[is.na(No_Business_interval) == T] = 0 
  operation_interval[is.na(operation_interval) == T] = 0 
  ```

  * Binning into category

  In my oppinion, missing is also information on that feature. I dont like delete or impute them directly. Sometimes, I'd like to keep them, making a new value for them. That is, I will create a new level named, "N/A" for the missing value. However, problems come out. If we use "N/A" to present the missing value, then the variable will be categorical feature. It is okay for the features with a small amount of values like gender. After created new level, gender can be "female", "male", "don't know". But for numeric variables like host_response_rate, value is numeric ranging from 0 to 100%. In this case, I created new level as "N/A" (not available), and binned the rate into two group, high rate(host_response_rate >= 80%) and low rate(host_response_rate < 80%). The information will be reducted but it is more effeciently for analysis and do not influence the analysis a lot. 

  ```R
  # transform missing value to "N/A"(not available). create a level for null value
  PB_3$host_response_time[is.na(PB_3$host_response_time)] <- "N/A"
  
  # host_response_rate {high: host_response_rate >= 80%}, {low: host_response_rate < 80%}, {N/A: not available}
  PB_3$host_response_rate <- as.numeric(sub("%","",PB_3$host_response_rate))/100
  summary(as.factor(PB_3$host_response_rate))
  PB_3$host_response_rate[PB_3$host_response_rate>= 0.8] <- "high"
  PB_3$host_response_rate[PB_3$host_response_rate< 0.8] <- "low"
  PB_3$host_response_rate[is.na(PB_3$host_response_rate)] <- "N/A"
  ```

  * Other feature engineering

  As I mention above, we can use monthly_price and weekly_price to create new features about the discount that host offered. In this step, we can not use the exact number from weekly_price and monthly_price. Because the two prices are calculated after we decide the daily price. That is, it will be higher when daily price is high. However, we can measure whether the airbnb provide the discount or not. If providing, we use the value as "offer discount", and if not, the value will be "no discount".

  ```R
  for (i in 1:length(PB_lm$weekly_price)) {
          if (is.na(PB_lm$weekly_price[i]) == T){
                  PB_lm$weekly_price[i] = PB_lm$price[i]*7
          }
  }
  weekly_discount_ratio = (PB_lm$weekly_price)/(PB_lm$price*7)
  weekly_discount_ratio[is.na(weekly_discount_ratio) == T] = 1
  #summary(weekly_discount_ratio)
  for (i in 1:length(weekly_discount_ratio)){
          if (weekly_discount_ratio[i] < 1 ){
                  PB_lm$weekly_price[i] = "offer discount"
          }
          else{
                  PB_lm$weekly_price[i] = "no discount"
          }
  }
  PB_lm$weekly_price = as.factor(PB_lm$weekly_price)
  #summary(PB_lm$weekly_price)
  ```



* **Filling in missing values automatically**

Sure, I mentioned that I do not like mean imputation in *Drop Columns with Missing Values*. But the situation is on condition that mean value is meaningless. Acturally, we imputate the missing value using the idea of maximum likelihood. Some features like host_has_profile_pic, presenting whether host has profile picture or not, have most value of "t". Most of host upload their profile picture on the sites. Therefore, we can use mode value to impute the missing value. 



## Inconsistent Data Entry



## Scale and Normalize Data



## Parsing Dates











