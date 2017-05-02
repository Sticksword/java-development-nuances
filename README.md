# Java Development Nuances
Feel free to fork and make a pull request! :)

### Typical Backend Flow
HTTP Request -> Serialize/Deserialize/Auth -> Controller -> Service/Business Logic Layer -> DAO/DAOImpl -> ORM framework (eg. Hibernate) -> DB


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
 
##### Language Misc:
* Spring basically has a 3 layer approach to developing APIs, @Repository, @Service, and @Controller (all 3 are Spring Components): http://stackoverflow.com/questions/6827752/whats-the-difference-between-component-repository-service-annotations-in
* Hibernate Query Language (HQL) Examples: http://www.codejava.net/frameworks/hibernate/hibernate-query-language-hql-example
* Another HQL guide that's a bit more recent: http://www.journaldev.com/2954/hibernate-query-language-hql-example-tutorial
* Hibernate Criteria Queries Tutorial/Examples: http://howtodoinjava.com/hibernate/hibernate-criteria-queries-tutorial-and-examples/#associations
* Okhttp Examples/Recipes: https://github.com/square/okhttp/wiki/Recipes
* Java 8 Lambdas: https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html
* Java 8 Stream examples: http://www.java2s.com/Tutorials/Java/Stream_How_to/List/Remove_element_from_List_with_removeIf_method.htm

 
### Effective Java Notes
#### Chapter 2: Creating and Destroying Objects
 1. Consider static factory methods instead of constructors -> can have names, not required to create new object each time invoked, can return an object of any subtype of their return type
 2. Consider a builder when faced with many constructor params, esp if they are optional -> combines Javabeans and Telescoping patterns and removes the flaws
 3. Enforce the singleton property with a private constructor or even better, an enum type -> have to ensure no multiple instances
 4. Enforce noninstantiability with a private constructor -> stops people from accidentally instantiating using a default constructor
 5. Avoid creating unnecessary objects -> reuse immutable objects, try to use static initializer for things that don't change in a class, prefer primitives to boxed primitives (eg. use long rather than Long)
 6. Eliminate obsolete object references -> avoid having obsolete references (to a machine, an allocated array will stay allocated regardless unless you specifically null out values you don't want)
 7. Avoid finalizers -> instead do try-finally blocks in combination with an explicit termination method

#### Chapter 3: Methods Common to All Objects
 8. Be careful when overriding `equals`, adhere to its general contract from the specification for `Object` [JavaSE6]
  * reflexive: for any non-null reference value `x`, `x.equals(x) must return `true`
  * symmetric: for any non-null reference values `x` and `y`, `x.equals(y)` must return the same as `y.equals(x)`
  * transitive: for any non-null reference values `x`, `y`, and `z`, if `x.equals(y)` and `y.equals(z)` are both true, then `x.equals(z)` must be true
  * consistent: your overriding `equals` method must be deterministic
 9. Always override hashCode when you override `equals`
 10. Always override `toString` -> makes the class more pleasant to use
 11. Override `clone` judiciously (?)
 12. Consider implementing `Comparable` with same precautions in mind as overriding `equals`

#### Chapter 4: Classes and Interfaces
 13. Minimize the accessibility of classes and members -> try to encapsulate (hide implementation information, only show public APIs for communication) so that the modules are decoupled
  * private: member is accessible only from the top-level class where it is declared
  * package-private: member is accessible from any class in the package where it is declared (this is the default behavior if no access modifier is specified)
  * protected: the member is accessible from subclasses of the class where it is declared and from any class in the package where it is declared
  * public: member is accessible from anywhere
  * note: instance fields should never be public! classes with public mutable fields are not thread-safe
 14. In public classes, use accessor methods, not public fields
 15. Minimize mutability => minimize complexity, maximize thread-safety (only drawback is that they require space, which is costly when creating many of these separate objects) Also, make every field final unless there is a compelling reason to make it nonfinal.
 16. Favor composition over inheritance
  * Note "inheritance" refers to "implementation inheritance" and not "interface inheritance"
  * Unlike method invocation, inheritance violates encapsulation -> subclass depends on the implementation details of its superclass for its proper function and when superclass's implementation changes, subclass may break
  * To avoid problems, instead of extending an existing class, give your new class a private field that references an instance of the existing class -> this design is called composition because the existing class becomes a component of the new one. Each instance method in the new class invokes the corresponding method on the contained instance of the existing class and returns the results -> AKA "forwarding" and the methods in the new class that do this are called "forwarding methods". Implementation would then be a wrapper class and a forwarding class.
  * Inheritance should only be appropriate when subclass really is a subtype of the superclass. In other words, a class B should extend a class A only if an "is-a" relationship exists between the two classes. ie. Is every B really an A?
 17. Design and document for inheritance or else prohibit it
 

#### Chapter 5

#### Chapter 6

#### Chapter 7

#### Chapter 8

#### Chapter 9

#### Chapter 10

### More Links and Resources
* https://www.reddit.com/r/java/comments/16ovek/understanding_when_to_use_jpa_vs_hibernate/
* http://softwareengineering.stackexchange.com/questions/211194/api-design-concrete-vs-abstract-approach-best-practices
* http://stackoverflow.com/questions/761194/interface-vs-abstract-class-general-oo
* http://stackoverflow.com/questions/29890562/initializing-list-of-objects-using-polymorphism

##### Notable design patterns
* https://www.tutorialspoint.com/design_pattern/factory_pattern.htm (interface with factory, call interface methods, don't need to know implementation details)
* https://www.tutorialspoint.com/design_pattern/flyweight_pattern.htm (similar idea in Python, make only what we need)
* https://www.tutorialspoint.com/design_pattern/builder_pattern.htm (one of the best ways to create a complex object, in small steps)

##### Mildly useful books
* https://www.manning.com/books/spring-in-action-fourth-edition
* https://www.amazon.com/Effective-Java-2nd-Joshua-Bloch/dp/0321356683
