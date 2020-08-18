# Difference between Hashtable and Collections.synchronizedMap
|Collections.synchronizedMap| Hashtable|
|---------------------------|----------|
|Methods are synchronized at block level using mutex|synchronization is on method level|
|The developer is allowed to pass another object of the mutex as a second argument by which the lock on the Map methods would be only on that Object and hence less restrictive| More restrictive than synchronized map locking in Collections.synchronizedMap can be done at object level while constructing Map.If object is not provided then|

# Difference between Hashtable and HashMap
|Hashtable|HashMap  |
|---------|---------|
|Hashtable is synchronized|HashMap is not synchronized. This makes HashMap better for non-threaded applications, as unsynchronized Objects typically perform better than synchronized ones.|
|Hashtable does not allow null keys or values|HashMap allows one null key and any number of null values|
|This wouldn't be as easy if you were using Hashtable|One of HashMap's subclasses is LinkedHashMap, so in the event that you'd want predictable iteration order (which is insertion order by default), you could easily swap out the HashMap for a LinkedHashMap|

# Difference between HashTables/SynchronizedMaps and ConcurrentHashMap

|HashTables/SynchronizedMaps|ConcurrentHashMap  |
|---------|---------|
|Whole Map is locked in case of HashTables/SynchronizedMaps.|locking particular portion/ segment|

# Fail fast and fail safe iterators

|Fail fast iterators|Fail safe iterators|
|---------|---------|
|If you try to modify the collection by means other than iterator's remove method ,then you get ConcurrentModificationException| Downside is ,it does not throw exception.They will not reflect the latest state of the collection.It requires extra memory as it clones the collection.|
|ArrayList, HashMap|CopyOnWriteArrayList, ConcurrentHashMap|

# Serialization
<pre>
    sequence of bytes = object’s data + information about the object’s type + the types of data stored in the object. 
    
    Main classes:
    ObjectInputStream and ObjectOutputStream
    
    Need of Serialization?
          1.when there is need to send your data(By data I mean objects and not text.) over network or to store in files
          2.Network infrastructure and your Hard disk are hardware components that understand bits and bytes but not Java objects.
    
    What happens:
        Case 1-What if an object has a reference to other objects
            Yes,You don’t have to explicitly serialize reference objects.When you serialize any object and if it contain any other object reference then Java serialization                   serialize that object’s entire object graph.
        Case 2:What if you don’t have access to reference object’s source code(e.g you don’t have access to above Address class)
            yes there is,You can create another class which extends address and make it serialzable but It can fails in many cases:
            What if class is declared as final
            What if class have reference to other non serializable object.
   
        Case 3:What if you still want to save state of reference object(e.g above address object):
            Java serialization provides a mechanism such that if you have private methods with particular signature then they will get called during serialization and                       deserialization so if we provide writeObject and readObject method of employee class and they will be called during serialization and deserialization of Employee                 object.
        
            *One thing should be kept in mind that ObjectInputStream should read data in same sequence in which we have written data to ObjectOutputStream in writeObject and                 readObject method.
        Case 4: What if superclass is Serializable?
             If superclass is serialzable then all its subclasses are automatically serializable.

            *If superclass is not Serializable then all values of the instance variables inherited from super class will be initialized by calling constructor of Non-                        Serializable Super class during deserialization process
            
       Case 6-What if superclass is Serializable but you don’t want subclass to be Serializable
             If you don’t want subclass to be Serializable then you need to implement writeObject() and readObject() method in subclass and need to throw                                      NotSerializableException from these methods.
            
       Case 7-Can you Serialize static variables?
              No, you can’t. As you know static variable is at a class level not at the object level and you serialize an object so you can’t serialize static variables.
              
              
       **Externalizable interface can be used in place of serializable if you want more control over serialization. You can read more about it at Externalizable in java.
       
 </pre>
 
 <pre>
 # Immutable object:
    An 'immutable' object is one whose instance cannot be changed once created.
    
    ## How to ensure ‘immutability’?
        -Make class itself final ,so that it can not be extented.
        
        -All fields (member variables) should be made private and final
        
        -Do not provide any ‘setter‘ methods (mutators)
        
        -initializing all non-primitive mutable fields via constructor by performing a deep copy;
        
        -Make defensive copies of any ‘mutable’ members which you might have as a part of your class i.e. do not provide direct access to the references of the mutable members.           Otherwise, the client API may unknowingly change the state of the mutable object which you returned which in turn will create loads of other issues
      
        When?
            You should consider immutability of your classes if you need:
            1.Safety:
                You, as a developer, can be sure that no one is able to change their state;
            2.Thread safety:
                Immutable objects do not need synchronization and are unharmed even during concurrent access by multiple threads.
            2.Simplicity: 
                Dealing with classes which would encapsulate your immutable object
            3.In Hash based collections for keys:
                Such immutable classes could be safely put inside the hash collections (like HashMap, HashSet etc) - of course, if equals() & hashCode() methods are overridden                     in a proper way.
                Immutable objects are good Map keys and Set elements, since these typically do not change once created.
            4.In caching:
                References to immutable objects can be cached as they are not going to change.
            
        Examples from JDK:
            The Java platform libraries contain many immutable classes,
                String,
                the boxed primitive classes,
                BigInteger,
                BigDecimal. 
        
 </pre>
 
 # Equals and hashcode contract:
    The part of the contract here which is important is: objects which are .equals() MUST have the same .hashCode().
 
       
 # Collections vs Streams:
 |Collections|Streams|
 |-----------|-------|
 |Can add and modify elements at any point of time| Can not remove or add elements once stream is created |
 |Elements can be accessed in any order | Can only be accessed sequencially|  
 |Eagerly constructed|Lazily constructed.Intermeditate operation are called only if terminal operator is called|  
 |Can be traversed any number of times| Can be traversed only once|
 ||Can only be traversed using internal iterator|
 
 
 # Stream API functions:
 
    Terminal operations: collect(), reduce() 
    
    -- map() , flatMap(),  distinct() ,count() , sorted() ,peek()//peek() is used to debug.
    -- Custom sorting sort(Comparator.comparing(Stundent::getName).reversed()).collect(Collectors.collect(toList()));
    -- filter()
    
 
 
 
# Covariant return types in Java.
<pre>
class A {} 
class B extends A {} 
  
class Base 
{ 
    A fun() 
    { 
        System.out.println("Base fun()"); 
        return new A(); 
    } 
} 
  
class Derived extends Base 
{ 
    B fun() 
    { 
        System.out.println("Derived fun()"); 
        return new B(); 
    } 
} 
  
public class Main 
{ 
    public static void main(String args[]) 
    { 
       Base base = new Base(); 
       base.fun(); 
  
       Derived derived = new Derived(); 
       derived.fun(); 
    } 
} 

Advantages:
    --  It helps to avoid confusing type casts present in the class hierarchy and thus making the code readable, usable and maintainable.
    --  We get a liberty to have more specific return types when overriding methods.
    --  Help in preventing run-time ClassCastExceptions on returns

</pre>
<pre>
# Exception handling in Java.

    1.If you extend Exception then it is "checked", i.e if you throw it, it must be caught or declared in the method signature.

    2.
        2.1 Unchecked exceptions extend RuntimeException and do not need to be declared or caught. 
        2.2 It is also possible to create an unchecked exception by extending Error or one of it subclasses, but these exceptions are by convention reserved for use by the JDK.
</pre>

# Difference between Inheritance and Composition in Java OOPS
    1) Static vs Dynamic
    When you use Inheritance, you have to define which class you are extending in code, it cannot be changed at runtime, but with Composition you just define a Type which you       want to use, which can hold its different implementation. In this sense, Composition is much more flexible than Inheritance.
    
    2) Limited code reuse with Inheritance
    with Inheritance you can only extend one class, which means you code can only reuse just one class, not more than one. If you want to leverage functionalities from multiple     class, you must use Composition. For example, if your code needs authentication functionality, you can use an Authenticater, for authorization you can use an Authorizer etc,     but with Inheritance you just stuck with only class, Why? because Java doesn't support multiple Inheritance.

    3) Unit Testing
    When you design classes using Composition they are easier to test because you can supply mock implementation of the classes you are using but when you design your class         using Inheritance, you must need parent class in order to test child class. Their is no way you can provide mock implementation of parent clas

    4) Final classes
    Composition allows code reuse even from final classes, which is not possible using Inheritance because you cannot extend final class in Java, which is necessary for             Inheritance to reuse code.

    5) Encapsulation
    Last difference between Composition and Inheritance in Java in this list comes from Encapsulation and robustness point of view. Though both Inheritance and Composition           allows code reuse, Inheritance breaks encapsulation because in case of Inheritance, sub class is dependent upon super class behavior. If parent classes changes its behavior     than child class is also get affected
    
  
# Why Java doesn't support multiple inheritance

    1.First reason is ambiguity around Diamond problem, consider a class A has foo() method and then B and C derived from A and has there own foo() implementation and now class     D derive from B and C using multiple inheritance and if we refer just foo() compiler will not be able to decide which foo() it should invoke. 

    This is also called Diamond problem because structure on this inheritance scenario is similar to 4 edge diamond, see below

             A foo()
               / \
              /   \
         foo() B     C foo()
              \   /
               \ /
                D
              foo()

       2) Second and more convincing reason to me is that multiple inheritances does complicate the design and creates problem during casting, constructor chaining etc and given        that there are not many scenario on which you need multiple inheritances its wise decision to omit it for the sake of simplicity. 
       
       
# Why String is Immutable or Final in Java

    1) Imagine String pool facility without making string immutable , its not possible at all because in case of string pool one string object/literal e.g. "Test" has referenced       by many reference variables, so if any one of them change the value others will be automatically gets affected i.e. lets say

    String A = "Test"
    String B = "Test"

    Now String B called, B.toUpperCase() which change the same object into "TEST", so A will also be "TEST" which is not desirable.
    2) String has been widely used as parameter for many Java classes e.g. for opening network connection, you can pass hostname and port number as string, you can pass database       URL as a string for opening database connection, you can open any file in Java by passing the name of the file as argument to File I/O classes.

    In case, if String is not immutable, this would lead serious security threat, I mean someone can access to any file for which he has authorization, and then can change the         file name either deliberately or accidentally and gain access to that file.
    
    3)Since String is immutable it can safely share between many threads which is very important for multithreaded programming and to avoid any synchronization issues in Java,         Immutability also makes String instance thread-safe in Java, means you don't need to synchronize String operation externally.
    4) Another reason of Why String is immutable in Java is to allow String to cache its hashcode, being immutable String in Java caches its hashcode, and do not calculate every       time we call hashcode method of String, which makes it very fast as hashmap key to be used in hashmap in Java. 
    5) The absolutely most important reason that String is immutable is that it is used by the class loading mechanism, and thus have profound and fundamental security aspects.     Had String been mutable, a request to load "java.io.Writer" could have been changed to load "mil.vogoon.DiskErasingWriter"
    
    
    
# Why default methods in Java 8?
    Default methods were added for backward compatibility for Old interfaces so that they can have multiple methods without breaking existing code.
    
    
