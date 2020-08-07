
# Benefits of Spring boot:
	1.It does not require you to deploy WAR files.For the same it  provides embedded tomcat.
	2.It creates standalone applications.
	3.It offers production ready features.
	
	
# Spring boot is Spring-based production ready project initializer.

# Spring features
	1.Dependency injection/IOC
	2.Transation



# What is Spring?
	provides comprehensive infrastructure support for developing Java applications.

	its packed with dependency injection and below out of box modules:
		Spring JDBC
		Spring MVC
		Spring Security
		Spring AOP
		Spring ORM
		Spring Test

	Before Spring,
		To insert a record we has write a lot of boilerplate code,
		with SpringTemplate of Spring JBDC module it reduces to a few lines of code 

# What is Spring boot?
		It is extension of Spring framework which eliminated the boilerplate configurations for setting up Spring boot applications.
		
		Features of Spring boot:
			-Opiniated starter dependencies to simplify build and applications configurations.
			-Embedded servers to avoid complexity in application development
			-Metrics, Health checks.
			-Automatic config for Spring functionality - whenever possible.
			
			
# What is opinionated view of a framework?
	If a framework is opinionated, it guides you into their way of doing things.
	


# Lets compare?
	Maven dependencies?
	
	1.develop a web application?
	Spring:	
		two dependencies
			spring-web
			spring-mvc

	Spring boot:
		just one dependency:
			spring-boot-starter-web
	
	2.testing libraries:
	Spring:
		dependencies needed:
			Spring test, Junit and Moickito
			
	Spring boot:
		just one dependency:
			spring-boot-starter-test
			
			
			
# Spring boot provides a number of starter dependencies for different modules:
	-spring-boot-starter-web
	-spring-boot-starter-data-jpa
	-spring-boot-starter-test
	-spring-boot-starter-security
	
	

	MVC configuration?
	configurations required to create jsp web application:
	
	Spring:
		-We have to define dispatcher servlet, mappings , and other supporting configurations in
			--web.xml
			--Initializer class
			-also define view resolver to resolve views
			
	Spring boot:
		just add web starter dependency and couple of properies in application.properies
		
		All configurations that we were doing in case of Spring is automatically done by
		Boot web starter ,through a process called auto-configuratio.
		
	
	Configuring template engine:
	

		
	Spring security configuration:
		
		
		
# Spring bean life cycle:
	Can be implemented in three ways:
		1.Using "init-method" and "destroy-method" in spring-config.xml file.
		2.Using @PostConstruct and @PreDestroy annotations.We have to additionally provide configuration for CommonAnnotationBeanPostProcessor
		2.Using implementing BeanPostProcessor interface in bean classes.
	
	How will you define order of execution when you have multiple BeanPostProcessors
		-By implementing Ordered interface in bean classes.
		
	

