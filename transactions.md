# Java Spring Study Notes

## TRANSACTIONS:  
* How?  
  * specify ```@Transactional``` on methods or classes  
  * __PIPELINE:__  
  1. create your ```@Entity``` and the ```@Repository``` which ```extends Repository<Entity, Long>```  
  2. define your ```@Service```, create an ```@Autowired``` repository and define a ```@Transactional``` method  
  3. the method will now be atomic when called from other methods.  
  * __NOTES:__
    * Spring creates the transaction by wrapping it into the "BEGIN TRANSACTION" statements, this is done only if you call the method from external calls! If you call it from within the method itself the @Transactional statement WILL NOT BE satisfied! (res: https://www.baeldung.com/transaction-configuration-with-jpa-and-spring)
    * As a general rule of thumb you don't want @Transactional on your DAO/Repository layer, but rather let it be managed from the Service layer. (res: https://stackoverflow.com/questions/30870146/transactional-annotation-not-working-in-spring-boot)

* You can specify the followings:  
  * isolation level
    * see: https://www.geeksforgeeks.org/transaction-isolation-levels-dbms/
  * readOnly flag
    * a hint for the persistence provider that the transaction should be read only
    * __NOTE:__ its just a hint the the transaction SHOULD NOT commit data to the database, if you do then it it not guaranteed that the commit will fail! (res: https://www.baeldung.com/transaction-configuration-with-jpa-and-spring)
  * propagation type  
  * execution timeout  
  * rollback rule  
