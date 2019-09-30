


### Tutorial about  to Use the Google API by Gustavo Bacab and Lisset Ruiz

First we need to get the Google API key In case we don't have a Google Cloud account you will need to create one.


 with your key (API key) is a unique code that is passed in to an API to identify the calling application or user. API keys are used to track and control how the API is being used.


## Important steps for the Api key:

1. we need to enter the google cloud platform (in case of not having an account it is necessary to create one).
2. Look for the option and Click on the drop-down menu and create the project for which you want to create an API key.
3. Find the menu button and select API and services and then Credentials.
4. In the Credentials section, select Create credentials and API Key.
    After stepping in, a box of the API key created appears immediately.

5. I suggest that you copy the api and keep it in a notebook, select close..
    It is very important to restrict the API key before using it in production.


 ## We are going to program.

We need the url that tells us the google documentation and import libraries (requests,json and pandas)

 ```


 'https://maps.googleapis.com/maps/api/place/nearbysearch/json?location={},{}&radius=2000&type={}&key={}'

 ```
 For this tutorial, we are using the Places API to find nearby places with     latitude and longitude as an input parameter, the radius (remembering that it is  in kilometers you have to multiply it by 1000), the most important type and key   , as it would allow you to make the request.
 you have to remember that when we create the parameters the separator is the  "&" symbol, so keep in mind
for this tutorial the output is a JSON, but it can also be an xml or body etc.

 
 ## we will enter the API key to your request
 With the api created in this section we need to enter it in this case I can as an example YOUR_API_KEY where you can your api.
in this case we enter the coordinates and we will put in radius 500 and remember that the type is what we are interested in looking for in this case food (restaurant)
```


https://maps.googleapis.com/maps/api/place/nearbysearch/json


  ?location=-33.8670522,151.1957362


  &radius=500


  &types=food


  &name=harbour


  &key=YOUR_API_KEY
  ```
 ### we will show the data
 The natural form of the json is not very visible and understandable so we will get to create a table to make it more orderly and readable.
In a function we declare the url.
```


def search_nearby_place(latitude, longitude, place, key):


    url = 'https://maps.googleapis.com/maps/api/place/nearbysearc/json?location={},{}&radius=2000&type={}&key={}'.format(


        latitude, longitude, place, key)


    res = requests.get(url)


    results = json.loads(res.content)


    return results     


```
Then call the function with the coordinates, remember that the type we will use is the type of restaurant and do not forget your API key.
```


res_data = search_nearby_place(20.988459, -89.736768, 'restaurant', YOUR_API_KEY)


```
We will create the table with the specific columns you need.
```


restaurantes_yucatan = pd.read_json(json.dumps(res_data['results']), orient = 'records')


restaurantes_table = restaurantes_yucatan[['name', 'place_id', 'rating', 'types','user_ratings_total']]


restaurantes_table


```
## we will use another Google Maps method [Places API] and the Google Maps library

When we use the Places API we need to use a string that will work as a url.
We will create functions.
functionality, and you don't have to work directly with the url.
```


    def find_place_id(placeName, location, key):


      placeName = urllib.parse.quote(placeName)


      url = 'https://maps.googleapis.com/maps/api/place/findplacefromtext/json?input={}&inputtype=textquery&locationbias=circle:600@{},{}&key={}'.format(placeName, location[0], location[1], key)


      res = requests.get(url)


      results = json.loads(res.content)


      return results  


  ```
Now we will use the GoogleMaps library.


don't forget to import the library then store your API key with the Client function, which will help you never write

and if we create another function we will need to add our API
```


import googlemaps


gmaps = googlemaps.Client(key= API_KEY)


```
we will use as an example what the exercise asks us with mccarthys etc
```


geocode_place_id = gmaps.find_place('McCarthys Irish Pub - Caucel', input_type ='textquery',


                                    location_bias='circle:600@20.999917,-89.682576')


```
Either method will obtain the same clear result that the second one is easier and shorter because in that new library it already includes all the functions we need in this project.

## Documentation and Resources 
[Get an API Key](https://developers.google.com/places/web-service/get-api-key)

[Google Maps Services Github](https://github.com/googlemaps/google-maps-services-python#api-keys)
[Get an API Key](https://developers.google.com/places/web-service/get-api-key)

[Places API](https://developers.google.com/places/web-service/search#FindPlaceRequests)

[Google Maps Services Github](https://github.com/googlemaps/google-maps-services-python#api-keys)

[Python Client for Google Maps Services Documentation](https://googlemaps.github.io/google-maps-services-python/docs/#module-googlemaps)

[Python Client for Google Maps Services Documentation](https://googlemaps.github.io/google-maps-services-python/docs/#module-googlemaps)
[google maps](https://cloud.google.com/maps-platform/?hl=es)





