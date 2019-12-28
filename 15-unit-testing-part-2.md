# Unit Testing Business Logic

Remember this picture from a few items back? 

![](12-backend-layers.png)

When Unit Testing, you want to make sure you test only 1 layer at a time. Anything "downstream" (toward the database) needs to be faked or mocked.   So if you want to test the controller, then you mock the business logic.  If you want to test the business logic, then you mock the DAO. 

This way you have total control over the inputs and output of the module. 

## Test ProductController by Mocking ProductService (Business Logic)

So we want to now have a unit test with the ProductController. So lets get started. 

1. Under the `/src/test` find the `com.houseawesome.RetailBackend.controllers` package

2. Add a Java class called `ProductControllerTest.java`

3. Replace the contents with this code:

```
package com.houseawesome.RetailBackend.controllers;

import com.fasterxml.jackson.databind.ObjectMapper;
import com.houseawesome.RetailBackend.models.dao.Product;
import com.houseawesome.RetailBackend.models.services.ProductService;
import org.junit.jupiter.api.Assertions;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.boot.test.mock.mockito.MockBean;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.MvcResult;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;

import java.math.BigDecimal;
import java.net.URI;
import java.net.URISyntaxException;
import java.util.UUID;

import static org.mockito.Mockito.any;
import static org.mockito.Mockito.when;

@WebMvcTest(ProductController.class)
public class ProductControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    ProductService productService;

    @Test
    public void testGetProductSuccess() throws URISyntaxException {

        try {

            // Pre-Test Setup
            UUID productID = UUID.randomUUID();
            Product returnedProduct = new Product();
            returnedProduct.setId(productID);
            returnedProduct.setName("Exterior Paint Black");
            returnedProduct.setPrice(new BigDecimal("224.99"));

            when(productService.getProductByID(any(UUID.class))).thenReturn(returnedProduct);

            final String baseUrl = "http://localhost:8080/products/" + productID.toString();
            URI uri = new URI(baseUrl);


            // Execute the call.
            MvcResult results = mockMvc.perform(MockMvcRequestBuilders.get(uri)).andReturn();

            
            // Validate the call was successful and the data that came back was as expected.
            Assertions.assertNotNull(results);
            Assertions.assertEquals(200, results.getResponse().getStatus());
            ObjectMapper mapper = new ObjectMapper();

            // Take the returned json, and turn it back into a Product object, then validate its content.
            Product finalProduct = mapper.readValue(results.getResponse().getContentAsByteArray(), Product.class);
            Assertions.assertEquals(finalProduct.getId(), returnedProduct.getId());
            Assertions.assertEquals(finalProduct.getName(), returnedProduct.getName());
            Assertions.assertEquals(finalProduct.getPrice(), returnedProduct.getPrice());


        } catch (Exception ex) {
            // if any errors are thrown, then fail.
            Assertions.fail();

        }
    }
}

```

4. Execute the test.   (Do you remember how?)

## What is happening in this test?

The code is a bit longer, but still fairly straight forward.  We want to test the Controller. So we create a fake downstream "ProductService" (Business Logic) stage some backend service data so we can return whatever we want to exercise the controller.  Then we create a fake webserver so we don't have to run a heavy service to run the test. 

Very powerful. 

## [NEXT -->](16-dao-database.md)