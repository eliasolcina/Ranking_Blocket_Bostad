# Ranking Objects on Blocket Bostad
### *Scraping  and Ranking Rental Objects from Blocket Bostad in Python using Selenium, BeautifulSoup and the Google Directions API.*

## Summary of the project
Blocket Bostad is one of Sweden's largest websites for publishing rental objects. In this project, the application scrapes 
all of the objects on Blocket Bostad based on five filtering options and creates a dataframe from the information.

Some of the information is used for further analysis, where the information gets ranked on different criteria, and all of the listing are later ranked based on the rank sum.

That is, the program scrapes relevant rental objects for the user, and ranks them based on three critera: 
 - How well the move in date for the rental object fits the users preference
 - How much rent you pay per square meter
 - Proximity to city centre in terms of access with public transport

Selenium is used to get around cookie-popups and press the "next page" button on the website, BeautifulSoup is used to actually retrieve the html-code and the Google Directions API calculated distances from rental objects to city centre (in kilometers and in minutes by public transport).

### Screenshot from the Blocket Bostad website:
Below is a screenshot from the Blocket Bostad website where there are two rental objects visible. The program scrapes the information from each and every one of these objects.


<img
  src="/blocketbostad_screenshot.png"
  alt="Blocket Bostad Screenshot"
  title="Blocket Bostad Screenshot"
  height = "600"
  width = "500" >

## Filtering options for the user
When the user runs the program, he or she will be presented with six questions:

- When do you want to move in to the rental object?
- In what area are you looking for a rental?
- Are you looking for a private or a shared rental, or both?
- Are you looking for a furnished or an unfurnished rental, or both?¨
- What is the minimal amount of rooms you are looking for?
- What is your max rent per month?

## Variable information:
#### Scraped variables:
- Address
- Area
- Accomodation type (house, apartment, room in apartment, etc.)
- Rooms
- Size in square meters
- Move in date
- Move out date
- Rent in SEK per month

#### Variables created from scraped data:
- Address + area in one string
- Rent per square meters

#### Variables created using the Google Directions API:
- Distance from rental object to city centre in the area (in kilometers)
- Travel time to city centre in the area by public transport

#### Three ranking variables in the dataframe:
- Rent/sqm_rank: Creating 10 quantiles out of the rent/sqm, where the lowest == 1 and highest == 10.
- Move_in_difference_rank: Number of days between the move in date and the desired move in date specified by the user, divided by 10 and rounded to the closest integer. This technique was used since rental objects specify move in date as "ASAP", which all converts to the same number of days. When the data is not (fairly) well distributed, quantiles are useless whereas the applied technique resulted in a "fair" rank.
- Distance_time_rank: Creating 10 quantiles out of the travel time to city centre with public transport, where the lowest == 1 and highest == 10.

The sum of these three ranking variables are stored in df['rank_sum'], and the rental object with the lowest rank_sum is considered the "best" object based on these attributes.

## Screenshot of the output
<img
  src="/df_screenshot.png"
  alt="Data Frame Screenshot"
  title="Data Fame Screenshot">

As you can see in the output above, all of the rankings have been summarized in rank_sum and can therefore be used as a column to sort the the objects in terms of attractiveness for the user.
