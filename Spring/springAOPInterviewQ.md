### 1. Describe Spring AOP?
**Spring AOP (Aspect Oriented Programming)** compliments **OOPs** in the sense that it also provides modularity. In OOPs, key unit is Objects, but in AOP key unit is aspects or concerns (simply assume stand-alone modules in your application). Some aspects have centralized code but other aspects may be scattered or tangled e.g. logging or transactions. These scattered aspects are called cross-cutting concern. A cross-cutting concern is a concern that can affect the whole application and should be centralized in one location in code as possible, such as transaction management, authentication, logging, security etc.

AOP provides the way to dynamically add the cross-cutting concern before, after or around the actual logic using simple pluggable configurations. It makes easy to maintain code in present and future as well. You can add/remove concerns without recompiling complete sourcecode simply by changing configuration files (if you are applying aspects suing XML configuration).

Spring AOP can be used by majorly 2 ways given below. But the widely used approach is Spring AspectJ Annotation Style.

1) By AspectJ annotation-style
2) By Spring XML configuration-style
