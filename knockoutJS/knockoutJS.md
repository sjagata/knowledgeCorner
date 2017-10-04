


### Knockout offers several useful variables that allow you to navigate between the context you are in to a parent or even the root context:

* **$root** - This accesses the root context (the ViewModel bound to Knockout) in any child context. This is handy when you are unsure of how many parent/child contexts are above
the one you are currently in.
* **$parent** - When you are in a child context, this will access the current context’s direct parent.
* **$parents** - This is similar to the $parent variable except that it contains an array of parent contexts to the context you are currently in. $parents[0] is the same as $parent. Similarly,
using $parents[$parents.length - 1] is the same as using $root.
* **$data** - This provides access to the current object your context is in. This is quite useful when you are in a context that is a variable and contains no properties.

