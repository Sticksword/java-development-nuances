# Java Development Nuances

### Typical Backend Flow
HTTP Request -> Serialize/Deserialize -> Controller (eg. Spring) -> Business Logic Layer -> DAO/DAOImpl -> ORM framework (eg. Hibernate) -> DB


### Java ORM Specifics
When accessing DB from an OOP language, typically need an ORM framework to do the conversion. For Java, there is Hibernate, JPA, and Hibernate with JPA.
* JPA -> both a specification and a bare bones implementation
 * reference: https://www.tutorialspoint.com/jpa/index.htm
* Hibernate -> standalone ORM framework that pre-dates JPA
 * uses EntityManager, JP-QL, Criteria Queries: https://docs.jboss.org/hibernate/entitymanager/3.5/reference/en/html/index.html
* Hibernate with JPA -> Hibernate but with JPA specs incorporated
 * uses SessionFactory, HQL, Criteria Queries (same name, diff implementation)
 * reference on what changed with JPA specs: http://stackoverflow.com/questions/20820880/hibernate-native-vs-hibernate-jpa
 * tl;dr you can switch out Hibernate's implementation of JPA with another implmentation (keep same annotations, etc.)
 * see more: http://stackoverflow.com/questions/9881611/whats-the-difference-between-jpa-and-hibernate
 
### Effective Java Notes
#### Chapter 2: Creating and Destroying Objects
 1. Consider static factory methods instead of constructors -> can have names, not required to create new object each time invoked, can return an object of any subtype of their return type
 2. Consider a builder when faced with many constructor params, esp if they are optional -> combines Javabeans and Telescoping patterns and removes the flaws
 3. Enforce the singleton property with a private constructor or even better, an enum type -> have to ensure no multiple instances
 4. Enforce noninstantiability with a private constructor -> stops people from accidentally instantiating using a default constructor
 5. Avoid creating unnecessary objects -> reuse immutable objects, try to use static initializer for things that don't change in a class 

#### Chapter 3

#### Chapter 4

#### Chapter 5

#### Chapter 6

#### Chapter 7

#### Chapter 8

#### Chapter 9

#### Chapter 10

### More Links and Resources
* https://www.reddit.com/r/java/comments/16ovek/understanding_when_to_use_jpa_vs_hibernate/
* http://softwareengineering.stackexchange.com/questions/211194/api-design-concrete-vs-abstract-approach-best-practices

