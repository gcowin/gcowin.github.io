Notes on D.I. (dependency injection)
------------------------------------
Q: Why not embrace dependency injection?
A: 

    It's misdirected and ironic, because it injects unneccesary dependencies. Instead of depending on a simple signature (f: a -> b), now you depend on everything in the interface and those dependencies. A way to scope, but as it turns out -- global. Needed due more to the inability to do effective composition, than to reduce/improve dependencies. 

    If your goal is reduced dependencies then D.I. is probably not the answer. From a dependency perspective, you can't get more minimal than f: a -> b.
    
    on a function signature as opposed to a whole interface and it's dependencies.  O.O. uses classes/objects to compose the app. Functional uses functions to compose the app. 

    By it's very name.

    This is a bit strong.

    Perhaps, think of it as a legacy way of dealing w/ context. Evolution beyond Von Neuman.

Q: What about D.I. claims of composition/reuse via injection?  
A: Not the most minimal strategy. The most minimal composition strategy: f : a -> b.

Q: Why does one something need to be referenced only to inject global variables into it?
A: Context. It is a tuff problem. D.I. is needed when dealing with object-oriented archs. It helps deal with separating signature from implementation. 


Issues
------
- violates single responsibility principle
- increases complexity
- runtime penalty for those that walk all classes in all DLLs
- if you inject something different then why use di?
- privates aren't private
- needless dependencies
- big constructors
- ironic

Alternatives
------------
partial functions
context parameters (ala scala)
    it is about abstracting over a context
reader monad
IO monad

AbstractFactory

Factory

Lambda's 

ServiceLocator
- Glorified static factory

Functional approaches you generally pass hof rather than a dependency to use later.

References
----------
Dependency rejection over dependency injection
http://blog.ploeh.dk/2017/02/02/dependency-rejection/


