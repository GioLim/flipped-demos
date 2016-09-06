# Ruby livecoding

## Regular expressions

## Collections and functional idioms (collections.rb)

* `each` is the basic iterator in Ruby. Among other things, allows a
data structure to manage its own traversal.  Don't think of writing a
loop with index; let the data structure enumerate its own elements.

* Try `each` on an array.
Give exampes of "expression oriented" tasks:
  * capitalize each word of a name: `name.split(//).map(&:capitalize).join(' ')`
  * reject words in a list that contain non-word characters: `list.reject { |word| word =~ /\W/ }`

* Now try `each` on hashes, filehandles; why does it work? Mix ins!
  * explain mixins, methods we've seen are in Enumerable, give a demo of Comparable, and talk about sorting.

* Demo: how would you sort bank accounts? 
  * Sorting is defined in Enumerable, but also relies on Comparable.  So
  the receiver of `sort` must be enumerable via `each`, and the elements
  of the collection returend by `each` must be comparable.
  * So - add comparison to bank accounts!
  * This is "Ruby thinking"

## Metaprogramming (currency.rb)

* International bank account demo: adding individual methods to Numeric to allow conversions like `3.euros`
* Use of `method_missing` to create a DRYer more general solution
  * Note use of mixin: we put our stuff in a module to keep it self-contained, then include (mix in) the module into `Numeric`, which is the ancestor of the various numeric classes `Fixnum`, `Float`, etc.

## Yield

* What does `each` really do?  It yields one element of a collection at
a time, handing it to the lambda (procedure) that is the argument of
`each` itself!
* Strings don't have a built-in sort function, but we know that sorting
is available in `Enumerable` as long as the receiver object can respond
to `each`, and each yielded object can respond to `<=>`.  Is this true
for strings?  Let's try it.
  * No `each`, so we must define it. What if we made strings yield one
  character at a time?  If each character was yielded as a string of
  length 1, we know we can compare them.  So we just need to define
  `each` on strings, and include `Enumerable` to get the `sort` method
