#Java APIs you should know
##Talks
- "Java APIs you should know", Hendrik Ebbers

##Null in Java
- NPE is "exception #1"
- Hendrik: "Java has null for a reason": Combobox with selectedID. If nothing is selected in combobox, null is OK in this case.  
- example: method with two Date as parameters and one line with access to both => if NPE is thrown, not sure if Date 1, Date 2 or both of them are null.
- better: 

    ````java
    if(first parameter == null) {throw NPE("1st parameter null")
    if(second parameter == null) {throw NPE("2nd parameter null")
    ````
- even better:
    ````java
    Objects.requireNonNull(object, message)
    ````
    Returns the object:
    ````java
    object = Objects.requireNonNull(object, message)
    ````
    => add this to constructor to construct only valid objects.
- even better: write a util-method to be used everywhere => see slides
- another solution: use default-value of Optional:
    ````java
    Optional.ofNullable(input).orElse("default");
    ````    
    If this is added at the begining of a method, it's nullsafe
- Optional usable in internal logic and as return-value, but NOT as method parameter because that way users of the API have to use Optionals even if they wouldn't do so otherwise. 
- NPE often occurs when autoboxing: bean with int and Entity with Integer => if entity-Integer is null and entity is transformed to Bean, NPE! Solution: Optional.ofNullable with 0 and default-value
- null should be handled early to have clean business logic
    
##Annotations
- TODO have a look at the slides, meybe simething interesting is there

##Plugins
- TODO have a look at the slides, meybe simething interesting is there

##Tasks
- Steven organize migrating all knowledge from here to other places (workshops, articles, talks, ...). Goal is to delete this repository and all its contents.
