# Layering the Backend

## Lost without a map

Imaging if you will that you and your friend are driving through the surface streets of Los Angeles. Your friend is driving, and you are asleep in the backseat.  You friend pulls into a random gas station and wakes you up and says "Your turn, i'm exhausted".  He promptly crawls into the backseat where you were and immediatly falls alseep. 

You have no idea where you are, no idea where you are going, and not sure if you turn left or right. 

You need a map! 

Well code is the same way. Code is more than just instructions. It is the detailed drawings of a complicated city.  And to move around a city, you need a map. Otherwise, you have zero clue if you should turn left or right. 

So lets continue to flush out our architecture diagram we created...


## All about the Layers

In technology, it is built with layers. It creates a [Abstraction Layer](https://en.wikipedia.org/wiki/Abstraction_layer). It lets the caller be unaware of the implementation details of the service.  As the developer, it helps us to "think" about software with focus.  It is very difficult for us humans, to hold the entire code set in our heads, so instead we need to break it down into layers and focus on getting that layer correct.  So now we are going to take the backend and split it into a few simple layers. This allows us to implement a [Seperation of Concerns](https://en.wikipedia.org/wiki/Separation_of_concerns) which is a critical pattern for larger software projects. 

So lets apply the MVC pattern to the Spring/Java Backend and subdivide it into a few layers with more specific names:

* Controller 
  * API Handler - this is the REST translation layer. Translate `GET /products/123456` and then determines which Model is needed to fetch the right data. This is the Air Traffic Controller.  These files will go into the `com.houseawesome.RetailBackend.controllers` package. 

* Model 
  
  * Business Logic (BL) - this is the core of the business app. This is where you should put the logic given to you by the business. "If the buyer is one of our known customers and has spent over $10,000 this month, then give them a 5% discount on the price of that product." These files will go under the `com.houseawesome.RetailBackend.models.services` package. 

  * Data Access Objects or DAO (Pronounced Dow, like Down, but without the 'n'). This is where the database is accessed and the data is fetched and packaged into [POJO](https://en.wikipedia.org/wiki/Plain_old_Java_object) to be returned to use in the Business Logic. These files will go under the `com.houseawesome.RetailBackend.models.dao` package 

* View
  * If the API is just JSON and data, then the view layer is very thin. If the API is serving HTML using templates, then the view becomes much more functional.  This functionality is packaged into Spring Boot so no extra package needed. 


When finished, it looks like this:

![](12-backend-layers.png)

This helps enforce Seperation of Concerns by using Abstraction Layers. Each part has a super specific job, and together they build a powerful model. I would venture to guess that almost all large business software is build like this or every similar even if it uses different names (cough... cough.. [Microsoft DAL](https://en.wikipedia.org/wiki/Data_access_layer))


## [NEXT -->](13-building-the-backend-layers.md)