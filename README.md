# Ranking Blocket Bostad
### *Scraping  and Ranking Rental Objects from Blocket Bostad in Python using Selenium, BeautifulSoup and the Google Directions API.*

### Summary of the project
Blocket Bostad is one of Sweden's biggest websites for publishing rental objects. In this project, the application scarpes 
all of the objects on Blocket Bostad based on a couple of filtering options and creates a pandas dataframe from the information.

Some of the information is used for further analysis, where the information gets ranked on different critera, and all of the listing are later ranked based on so called the rank sum.

### Screenshot from the Blocket Bostad website:
<img
  src="/blocketbostad_screenshot.png"
  alt="Blocket Bostad Screenshot"
  title="Blocket Bostad Screenshot"
  height = "600"
  width = "500" >

### Variable information
#### Scraped variables
- Address
- Area
- Type
- Rooms
- Size in square meters
- Move in date
- Move out date
- Rent in SEK per month

#### Variables created from scraped data
- Address + area in one string
- Rent per square meters

#### Variables created using the Google Directions API
- Distance from rental object to city centre in area (in kilometers)
- Travel time to Stockholm City by public transport

#### Three ranking variables in the dataframe:
- Rent/sqm_rank: Creating 10 quantiles out of the rent/sqm, where the lowest == 1 and highest == 10
- Move_in_difference_rank: Number of days between the move in date and the desired move in date specified by the user, divided by ten and rounded to the closest integer
- Distance_time_rank: Creating 10 quantiles out of the travel time to city centre with public transport, where the lowest == 1 and highest == 10

The sum of these three ranking variables are stored in df['rank_sum'], and the rental object with the lowest rank_sum is considered the "best" object based on these attributes.
