# Create the DAO Layer

![](12-backend-layers.png)

The DAO has one main job.  Handle the interaction with the database.  So now we are going to flush out how the DAO does this. 

I'm going to assume at this point you are comfortable creating java files in specific packages at this point.  So the instructions at this point are going to be more straight, and to the point. Reference back to early units if you need more detailed instructions. 

## Create ProductDAO.java

The DAO has final responsibilites for executing any SQL queries and returning the resulting Java object. 

In the `com.houseawesome.RetailBackend.models.dao` package, create a ProductDAO.java with this content:

```
package com.houseawesome.RetailBackend.models.dao;

import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.stereotype.Component;

import javax.sql.DataSource;
import java.util.UUID;

@Component
public class ProductDAO {

    JdbcTemplate jdbcTemplate;

    public ProductDAO(DataSource dataSource) {
        jdbcTemplate = new JdbcTemplate(dataSource);
    }

    public Product getProductById(UUID id) {
        return jdbcTemplate.queryForObject("select * from products where id = ?", new Object[] { id }, new ProductMapper());
    }
}
```


## Create ProductMapper.java

The ProductMapper is just a simple helper function to map the resultSet that comes back from the JDBC Driver and map it to java data objects like Product. Nothing fancy. 

In the `com.houseawesome.RetailBackend.models.dao` package, create ProductMapper.java ith this content:

```
package com.houseawesome.RetailBackend.models.dao;

import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.UUID;

import org.springframework.jdbc.core.RowMapper;

public class ProductMapper implements RowMapper<Product> {

    public Product mapRow(ResultSet resultSet, int i) throws SQLException {

        Product product = new Product();
        product.setId(resultSet.getObject("id", UUID.class));
        product.setName(resultSet.getString("name"));
        product.setPrice(resultSet.getBigDecimal("price"));
        return product;
    }
}
```

## Update ProductService.java

Open the `ProductService.java` and replace its contents with this one. This wires the service to the underlying DAO object. 

```
package com.houseawesome.RetailBackend.models.services;

import com.houseawesome.RetailBackend.models.dao.Product;
import com.houseawesome.RetailBackend.models.dao.ProductDAO;
import org.springframework.stereotype.Service;

import java.util.UUID;

@Service
public class ProductService {

    ProductDAO productDAO;

    public ProductService(ProductDAO productDAO) {
        this.productDAO = productDAO;
    }

    public Product getProductByID(UUID id) {

        // This is where business logic will go.
        // if any decisions need to be made about products, it goes here.
        // more important on creates, updates, and deletes.
        Product product = productDAO.getProductById(id);

        return product;

    }
}

```

## Update application.properties

Look inside the `src/main/resources/` and you will find a file called `application.properties`.  This file is very important to spring projects.  It is where you put configuration for the project. It is read when the application starts. It should be empty at this point. So add it:

```
spring.jpa.hibernate.ddl-auto=none
driver=org.postgresql.Driver
spring.datasource.url=jdbc:postgresql://localhost:5432/retaildb
spring.datasource.username=svc_retail
spring.datasource.password=RetailRules123
```

## [NEXT -->](18-run-the-app.md)



