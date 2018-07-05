## Cache in Prisma

#### Using Cache in Prisma

For caching Prisma uses Caffeine right now but the development of this library sub-project is agnostic to any other tool. There are three variants of cache implementation that you can use in Prisma.

1. Unbounded-Synchronous    
1. Bounded-Synchronous
1. Bounded-Asynchronous

To get an instance of a cache you can import [Cache](https://github.com/prismagraphql/prisma/blob/master/server/libs/cache/src/main/scala/com/prisma/cache/Cache.scala) object -- note, you might have to import this sub-project in your sub-project. With the Cache object, you can get one of the three instances of the Cache implementation. 

PS: Bounded-Synchronous and Bounded-Asynchronous use LFU replacement policy, and you can set the initial capacity and maximum capacity for the cache. 

#### Adding a new Cache Library

If you are looking to add another caching library like cache2k or guava cache, that can be added very easily. You need to extend trait [Cache](https://github.com/prismagraphql/prisma/blob/1d2203e05d00ac033fb4e9534e6ddb0799267ddf/server/libs/cache/src/main/scala/com/prisma/cache/Cache.scala#L19) if you are implementing a Synchronous cache or [AsyncCache](https://github.com/prismagraphql/prisma/blob/1d2203e05d00ac033fb4e9534e6ddb0799267ddf/server/libs/cache/src/main/scala/com/prisma/cache/Cache.scala#L31)  if you are looking for an Asynchronous cache. You can create a function in [Cache](https://github.com/prismagraphql/prisma/blob/master/server/libs/cache/src/main/scala/com/prisma/cache/Cache.scala) object to access an instance of your implementation.

**Dependencies**
1. [Caffeine](https://mvnrepository.com/artifact/com.github.ben-manes.caffeine/caffeine)
1. [JSR 305](https://mvnrepository.com/artifact/com.google.code.findbugs/jsr305) (@NotNull used by Caffeine)
1. [Java8-Compat](https://mvnrepository.com/artifact/org.scala-lang.modules/scala-java8-compat) (Used for interoperability between Java and Scala because Caffeine Uses Java at core)
1. [ScalaTest](https://mvnrepository.com/artifact/org.scalatest/scalatest)
1. [ScalaCheck](https://mvnrepository.com/artifact/org.scalacheck/scalacheck)
 





   