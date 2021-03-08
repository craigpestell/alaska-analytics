# Alaska Analytics
Capture user flight search data on alaskaair.com to answer:
- flight search conversion rate
- cost in miles to conversion rate ratio
- number of searches for flights not offered by airport and/or date

## Individual flight search result conversion rate 
To answer this question we need to track each time a flight appears in a search result, and each time a flight is purchased, after being chosen from a search result. 

## How does the cost in miles affect the guest's willness to purchase
To answer this question we need to track the cost in miles of each flight that appears in a search result, and the cost in miles of each flight purchased after being chosen from a search result.

## How many times does a guest attempt to search for a destination that we do not serve for the given airport or date?
To answer this question we need to store the departure and arrival airports, and departure and arrival dates for searches where no results are found.


## Implementation

To capture the data necessary to answer these questions, there are three components necessary: the capturing of user search data, the storage of the search data, and the reporting tool that will analyze and intergpret the data.

### Capturing search results

The search result data can be captured from the browser or from the server. Each method has advantages and disadvantages.

See search.json, search_no_results.json, add_to_cart,json and checkout.json for examples of the data to be collected.

**Client-side** data capture requires a javascript module installed on the website, that is invoked when a search is executed, and/or when search results are returned to the user. The module could read url parameters, the http request body, local storage, Vuex, GraphQL, or the DOM to collect the data, and the data would be sent to an analytics platform via AJAX request. Flight purchases would be tracked as well.

**Server-side** would involve capturing the HTTP request of a user's search, and the subsequent search results on a service (Node.js), and sending that information to the analytics platform, as well as flight purchase data.

Implementing analytics on the client would allow using tag management tools like Tealium to manage third party data collection, whereas server-side data is not usually accepted by third parties.  Collecting data on the client also provides the ability to create a javascript module that usable by third parties to send analytics data to Alaska airlines.


## Data storage / structure

The search data does not need to stored on an in-house database to provide the answers we want, but doing so would allow the data to be used by others besides the analytics platform.

Database structure (see database.drawio)

**Option 1: Store search data only in analytics platform**

Database contains user accounts, user's purchased itineraries.  Searches and search results are stored in analytics platform

- less development and maintenance
- difficult to migrate analytics data to another provider

**Option 2: Store search data in database and analytics platform**

Database contains user accounts, user's purchased itineraries, as well as search data
    
- data retention and in-house data storage allows data to be used outside the analytis platform, and allows for migration to other analytics providers
- more development and maintenance

## Reporting

Reports can be configured via an analytics provider platform like Adobe Analytics, or in-house reporting tools