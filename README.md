# Vue-Event-Search-Practice
The practice application to make search feature in vue using Vue JS using a search API from Jublia. 

## Purpose of the application
The purpose of this application is to browse all the exhibitors (identified by exhibitors ID) in a certain event (identified by event_id) which the event is hosted by a client (identified by client_id). Also, to bookmark the company or to message or read a message from a company, so the client could communicate with the company and can decide whether the client will invite the company again for the next event or not, or other purposes.

## The application features
1. Load all the exhibitors from the API call, then store them to the local storage. If local storage is not empty, then the application will load the data from the localstorage.
2. Search the exhibitors by the exhibitor name real time, by using "computed" in Vue JS.
3. Filter the exhibitors by the first letter of its name
4. Bookmark the exhibitor, change the indicator by identify the exhibitor_id of each exhibitor
5. Change the message indicator of each exhibitor item

## Brief explanation of the API
The link of API is:
https://api.jublia.com/buzz/v2/directory/search

It takes 2 parameters:
1. event_id : the ID of the searched
2. client_id : the ID of the client

## Brief explanation of the API response
The response of this API call is "searchResult" JSON object. It has attributes listed below:
1. "attributes"
"attributes" is the collection of attribute of the exhibitors. "attributes" contains the "Category", which lists the category products of the company, "Booth No." which contains the information of the booth number of the exhibitor, "Country" which shows where the exhibitor resides, and "Industry" shows the industry category of the exhibitor

2. "bookmark"
Indicates whether this company is bookmarked by the client or not. If bookmarked, the value of "bookmark" is set to the value of the client_id, if not then the value is 0. Has an integer data type.

3. "booth"
The booth number of the exhibitor in a certain event. Has a string data type. Companies which are the role/group is sponsor don't have a booth.

4. "company_description"
A short description of a company or exhibitor. Has a string data type.

5. "company_name"
The name of company or exhibitor. Has a string data type.

6. "group"
The role of a company in an event, in this case could be "Exhibitors" or "Sponsors". Has a string data type

7. "id_exhibitor"
The ID of the company, which is used as a unique identifier for each company. Has an integer datatype.

8. "logo"
The URL of logo image of the company. Has a string data type

9. "messaged"
Indicates if this company has messaged or sent a new message to the client or not. If value = 1, then the company has messaged the client, if 0 then the company hasn't messaged the client. Has an integer data type, but it could be a boolean also (1 represents true, 0 represents false)
## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
