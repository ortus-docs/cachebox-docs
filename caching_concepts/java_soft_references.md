# Java Soft References

> "In the past, developers didn't have much control over garbage collection or memory management. Java2 has changed that by introducing the java.lang.ref package. The abstract base class Reference is inherited by classes SoftReference, WeakReference and PhantomReference. SoftReferences are well suited for use in applications needing to perform caching."


<img src="../images/cachebox_softreference.png">

Why is this? Well, a soft reference is nothing but a wrapper class that wraps an object in memory. Whenever the JVM requires memory and runs its reference rules, it can detect these soft references and decide to purge them if it meets the garbage collector rules. If it purges them, the wrapped object inside of the soft reference is marked for collection, but the java soft reference itself still exists. Therefore, the programmer can determine if the object inside the reference exists or not. If it does not exist, it means the object was garbage collected and I have no more object. I won't go into the implementation semantics of the cache, just theory. Please visit the references to understand more of how the ColdBox cache was built. 

In summary, soft references are what determine if an object is still available or not. CacheBox cache can then run maintenance on itself and clean out all of its references for you if you are using the `ConcurrentSoftReferenceStore` object store.

## Useful Resources
* http://java.sun.com/j2se/1.5.0/docs/api/java/lang/ref/SoftReference.html
* https://www.rallydev.com/community/engineering/java-references-strong-soft-weak-phantom