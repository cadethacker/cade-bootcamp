# **RUN THE APP**

This is an exciting moment.  If everything worked as expected, then you should be able to run the app and fetch data from end to end. 

1. Start the App (remember how?)
2. Use whatever api tool you want (curl, postman, etc) and hit:

```
GET http://localhost:8080/products/9c9ffd03-707d-4e2f-ab5c-ac0e7ffca3b4

And you should get back:

{
    "id": "9c9ffd03-707d-4e2f-ab5c-ac0e7ffca3b4",
    "name": "Light Blub",
    "price": 2.98
}

BOOOO YAAAAY!!!!!!!!!
```


3. Try a different product:

```
GET http://localhost:8080/products/e78a6b2d-760e-42e4-a51c-66abdac4e0fb

And you should get back:

{
    "id": "e78a6b2d-760e-42e4-a51c-66abdac4e0fb",
    "name": "Nail Gun",
    "price": 29.98
}

WHOO HOOO!!!!
```

This is a huge moment.  Stand up, do a dance of joy. Maybe a few fist pumps in the air. 

You created your first real, business ready Spring Boot Business application. This is no mere toy to learn on. This thing is ready to build out, scale, and build your Retail Empire on! 


![](tony-stark-success.gif)


## [NEXT -->](19-add-service-unit-test.md)