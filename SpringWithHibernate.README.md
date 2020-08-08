## Spring with hibernate:

# What is autoconfiguratin?
You understand by knowing how you were able to create rest API just by adding Web dependency.
You get the idea by getting all beans from context and printing them on console.

# Property to keep log at DEBUG level?

logging.level.org.springframework=DEBUG

# What core problem Spring framework solves.
1.Dependency injection throught IOC.Which again increased testability of code.
2.Integration with other framework.

# What core problems of Spring framework is solved by Spring boot.

1.Auto configuration. It  does best on jars in class path.
	like is spring web dependency is in class path
	then 
		1.Dispatcher servlet is configured
		2.View resolver is configured automatically.
		
	if you have Spring Data JPA in class path,
	then,
		1.data source
		2.entity soource
		3.transaction mangager are auto configured.
		
		
Spring boot starters:
	Web:
	It used for developing web applications as well RESTfull web services.

Actuators:
	gives
	1.beans configured
	2.how many times a specific service has been called or failed.
	

 Enabling management endpoints will have performace impact:
management.endpoints.web.exposure.include=*  
 *It has performace impact

Spring bool dev tools:


# Which InheritanceType mapping to use in Inheritance hierachy?
	Use TABLE_PER_CLASS when performace is the concern.
		Here you will have to make columns nullable.
	Use JOINDED when data integrity is the main concern.
		Here performace will be slow due to join while fetching the data.
	
	
# With JPA/JPQL we worry about only Entities not course.


# Transaction Management : ACID properties

	A-Atomicity-  All changes done by a transation should completely successful ,or changes should be reverted back.For
					example, if a transaction has 10 steps then all suceed or changes by all of them should be reverted back
	C-Consistency-Any transaction should leave system in consistent state
	I-Isolation- How changes within a transaction are visible.
	D-Durability-Once transaction is complete, all changes made should be persisted and it should remain even after system failure.
	
