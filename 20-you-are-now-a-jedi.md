# You are now a JEDI...


To quote Luke Skywalker...

![](old-luke-skywalker.jpg)

The map is in place, you have the pattern, and you have Google.  What can you do from here? 

I have some suggestions:

1. Implement `GET /products` and have it return all products. 

2. Implment `GET /products/{id}` with an id that doesn't exist or an invalid ID. What should happen? What Status Code? Can you write a unit test that validates the functionality?

2. Implement `GET /products` pass in `?q=price>50` which returns all prices with price > $50

3. Implement `POST /products BODY: { name, price }` and have add the product to the database. 

4. Implment `PUT /products/{id} BODY: { id, name, price }` and have the product updated in the database. 

