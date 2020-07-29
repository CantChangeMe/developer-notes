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
 |Early constructed|Lazily constructed.Intermeditate operation are called only if terminal operator is called|  
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

</pre>
