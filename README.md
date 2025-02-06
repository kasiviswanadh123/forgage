# forgage
data model

#Creating an Entity Class (e.g., User Entity)
package com.yourproject.entities;

import javax.persistence.*;

@Entity  // Marks this class as a JPA entity
@Table(name = "users") // Maps to the "users" table
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY) // Auto-generates ID
    private Long id;

    @Column(nullable = false) // Ensures this field cannot be null
    private String name;

    @Column(unique = true, nullable = false)
    private String email;

    @Column(nullable = false)
    private String password;

    // Constructor
    public User(String name, String email, String password) {
        this.name = name;
        this.email = email;
        this.password = password;
    }

    // Default constructor (JPA requires a no-args constructor)
    public User() {}

    // Getters and Setters
    public Long getId() { return id; }
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    public String getEmail() { return email; }
    public void setEmail(String email) { this.email = email; }
    public String getPassword() { return password; }
    public void setPassword(String password) { this.password = password; }
}

#use JPA annotations like @OneToMany, @ManyToOne, etc.
ex: A User has multiple Orders (One-to-Many Relationship)
@Entity
@Table(name = "orders")
public class Order {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @ManyToOne  // Many orders belong to one user
    @JoinColumn(name = "user_id", nullable = false)
    private User user;

    @Column(nullable = false)
    private String product;

    @Column(nullable = false)
    private Double price;

    // Constructor
    public Order(User user, String product, Double price) {
        this.user = user;
        this.product = product;
        this.price = price;
    }

    // Default constructor
    public Order() {}

    // Getters and Setters
    public Long getId() { return id; }
    public User getUser() { return user; }
    public void setUser(User user) { this.user = user; }
    public String getProduct() { return product; }
    public void setProduct(String product) { this.product = product; }
    public Double getPrice() { return price; }
    public void setPrice(Double price) { this.price = price; }
}
