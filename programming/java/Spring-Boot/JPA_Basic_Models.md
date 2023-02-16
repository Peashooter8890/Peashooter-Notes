# JPA and Basic Models

## Introduction to JPA
JPA, or Java Persistence API, is a design framework that allows us to have easier backend-database interactions without having to integrate SQL queries in our code - it basically automatically generates the queries for us. 

JPA maps properties of a class into columns of a database, and the values of the rows of the database will be the arguments of any initialized objects of that class. 

Hibernate is the implementation of JPA in code form - we can define a persistence.xml or hibernate.cfg.xml file to define that we are using hibernate stuff (and the IDE or package managers can install hibernate stuff in the local machine). 

To use JPA in your project, define a hibernate file, install extra dependencies and stuff, then write this code in your class file:

```java
import javax.persistence.*
```

which tells the compiler/machine to use JPA architecture in the class. 

Use @Entity to declare that a class is an entity to be mapped to the database table. This allows the class to use hibernate. 
```java
@Entity
```

## Simple Application of JPA
Here is one example on making a class model using JPA. We are declaring a "product" class in a simple ecommerce setting - once the user buys the product, they can keep it or sell it when the market price changes. 

it should have properties like name, price, mapping to a bigger collection class, purchase property, etc. 

```java
// We create a package of this class to import it to other files
package <directory>;  

// Imports @JsonIgnoreProperties - will be explained in the code later
import com.fasterxml.jackson.annotation.JsonIgnoreProperties;  

// Imports lombok which automatically generates and calls methods like @Getter and @Setter - makes things very convenient when requesting or changing data
import lombok.*;  

// Allows support for JPA
import javax.persistence.*;  

// Getter requests data, setter modifies data
@Getter  
@Setter  

// Makes strings possible in java - without them, we would have to manually create char arrays
@ToString  

// Slightly changes syntax of declaring this class on a seperate file. It diverges from the traditional method of <Class object = new Class(var_1,var_2,...var_n)>
@Builder  

// Automatically defines and builds anonymous or argument-given constructors
@AllArgsConstructor  
@NoArgsConstructor  

// Declares that the class will be mapped into a table
@Entity  

// Sets name of table as "product"
@Table(name = "product")  

// When JPA/hibernate outputs their data in JSON format, these two properties will be included which could potentially cause errors. So we are making it ignore these properties when potential JSON conversion/modeling happens. 
@JsonIgnoreProperties({"hibernateLazyInitializer", "handler"})  

public class Product {  
		// This basically automatically generates the ID of a product sequentially whenever it is generated. So the first ever generated product will have ID of 1, second one will have ID of 2, so forth...
        @Id  
        @GeneratedValue(strategy =  GenerationType.IDENTITY)  

		// @Column declares property as a column in database and names it
		@Column(name = "product_id")  
        private int id;  
        @Column(name = "product_name")  
        private String name;  
        @Column(name = "market_price")  
        private int marketPrice;  
        @ManyToOne  
        // When product is not in an account yet, nullable = true allows the column to be null
        @JoinColumn(name="account_id", nullable=true)  
        private Collection collection;  
        @ManyToOne  
        @JoinColumn(name="purchase_id", nullable=true)  
        private Purchase purchase;  
}
```
