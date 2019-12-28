# Unit Test the Service Layer

In real Unit Testing, you build the test first, and then add the functionality, but for new developers, this presents a chicken-and-egg problem.  How do you test something that you have no clue how it works?  

You know you have matured as a developer when you feel comfrotable writing the unit test first, and then implementing the code.  Keep pushing yourself. 

For the moment, though, we are going to add unit tests after the feature, but once you get the design patterns down, it is much easier to flip this order. 

![](12-backend-layers.png)

In the previous effort, we created a unit test for the controller, by mocking the Service (Business Logic).  Now we are going to Unit test the Service (Business Logic) by mocking the DAO. 


## Create the Test

1. In the `src/test/java`, create a new package called `com.houseawesome.RetailBackend.models.services;`

2. In that package create a java file named `ProductServiceTest.java` with the below code


```
package com.houseawesome.RetailBackend.models.services;

import com.houseawesome.RetailBackend.models.dao.Product;
import com.houseawesome.RetailBackend.models.dao.ProductDAO;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

import java.math.BigDecimal;
import java.util.UUID;

import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.mockito.Mockito.*;

public class ProductServiceTest {


    private ProductDAO productDAO;
    private ProductService productService;

    @BeforeEach
    public void beforeEach() {
        // create the productService and pass in the mock.
        // the product service doesn't know any different or care.
        // I love mocks.
        productDAO = mock(ProductDAO.class);
        productService = new ProductService(productDAO);
    }

    @Test
    public void getProductByIDTest()
    {

        // Stage some data in the productDAO mock
        UUID productID = UUID.randomUUID();
        Product stagedProduct = new Product();
        stagedProduct.setId(productID);
        stagedProduct.setName("Exterior Paint Black");
        stagedProduct.setPrice(new BigDecimal("224.99"));

        // pre-stage the fake data in the mocked DAO layer.
        when(productDAO.getProductById(productID)).thenReturn(stagedProduct);

        //call the service
        Product returnedProduct = productService.getProductByID(productID);

        assertEquals(returnedProduct.getId(), stagedProduct.getId());
        assertEquals(returnedProduct.getName(), stagedProduct.getName());
        assertEquals(returnedProduct.getPrice(), stagedProduct.getPrice());

        // check that the productDAO.getProductByID(...) was 
        // called exactly once. this is a great way to catch 
        // unintended side effects. 
        verify(productDAO, times(1)).getProductById(productID);

    }

}

```

3. Now run all the tests (there are now 4), and they should all pass! 


## [NEXT -->](20-you-are-now-a-jedi.md)