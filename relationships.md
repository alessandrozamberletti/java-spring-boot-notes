# Relationships

## @OneToOne -> 1to1
```java
@Entity
public class Library {
 
    @Id
    @GeneratedValue
    private long id;
 
    @Column
    private String name;
 
    @OneToOne
    @JoinColumn(name = "address_id")
    @RestResource(path = "libraryAddress", rel="address")
    private Address address;
     
    // standard constructor, getters, setters
}
```
```java
@Entity
public class Address {
 
    @Id
    @GeneratedValue
    private long id;
 
    @Column(nullable = false)
    private String location;
 
    @OneToOne(mappedBy = "address")
    private Library library;
 
    // standard constructor, getters, setters
}
```
* the entity with the foreign key in its table is the child
* the parent should use ```@OneToOne(mappedBy = "address")```
  * ```mappedBy``` tells JPA that rankings are mapped by the artist entity on the ranking object
* the child should have ```@OneToOne``` and ```@JoinColumn(name = "address_id")```
  * this tells JPA that "Address" is mapped to ranking via the "address_id"
* __SUMMARY__ ```@OneToOne``` on both, ```mappedBy``` on table without the foreign key (parent), ```@JoinColumn``` on table with the foreign key (child)

## @ManyToOne -> Nto1
```java
@Entity
public class Book {
 
    @Id
    @GeneratedValue
    private long id;
     
    @Column(nullable=false)
    private String title;
     
    @ManyToOne
    @JoinColumn(name="library_id")
    private Library library;
     
    // standard constructor, getter, setter
}
```
```java
public class Library {
  
    //...
  
    @OneToMany(mappedBy = "library")
    private List<Book> books;
  
    //...
  
}
```
* the entity with the foreign key in its table is the child
* the parent should use ```@OneToMany(mappedBy = "library")```
  * ```mappedBy``` tells JPA that rankings are mapped by the library entity on the book object
* the child should have ```@ManyToOne``` and ```@JoinColumn(name = "library_id")```
  * this tells JPA that "Address" is mapped to ranking via the "address_id"
* __SUMMARY__ ```@OneToMany``` on parent - ```@ManyToOne``` on child, ```mappedBy``` on table without the foreign key (parent), ```@JoinColumn``` on table with the foreign key (child)

## @ManyToMany -> NtoN
```java
@Entity
public class Author {
 
    @Id
    @GeneratedValue
    private long id;
 
    @Column(nullable = false)
    private String name;
 
    @ManyToMany(cascade = CascadeType.ALL)
    @JoinTable(name = "book_author", 
      joinColumns = @JoinColumn(name = "book_id", referencedColumnName = "id"), 
      inverseJoinColumns = @JoinColumn(name = "author_id", 
      referencedColumnName = "id"))
    private List<Book> books;
 
    //standard constructors, getters, setters
}
```
```java
public class Book {
  
    //...
  
    @ManyToMany(mappedBy = "books")
    private List<Author> authors;
  
    //...
}
```



## References
* https://www.baeldung.com/spring-data-rest-relationships
* https://tenmilesquare.com/spring-boot-jpa-relationship-quick-guide/
