### Q) What are “static initializers” or “static blocks with no function names”?
When a class is loaded, all blocks that are declared static and don’t have function name (i.e. static initializers) are executed even before the
constructors are executed. As the name suggests they are typically used to initialize static fields.
