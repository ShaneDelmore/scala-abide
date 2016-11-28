# Extra rules package [rules/extra](/rules/extra/src)

The rules found in this package form a complement to the [rules/core](/wiki/core-rules.md) package and provides rules that are generally not as widely accepted as those found in core. One will typically not use all the rules provided by this package, but some may be of interest and can be selectively enabled when necessary.

## Fixing the overriden method parameter names

name : **fixed-name-overrides**  
source : [FixedNameOverrides](/rules/extra/src/main/scala/com/lightbend/abide/extra/FixedNameOverrides.scala)

When overriding a method, it can be worthwhile to keep the argument names (and ordering) to make sure the source remains clear and easily readable when traversing a hierarchy. This rule will enforce such consistent naming and provide warnings when the names differ on method override.

## Usage of isInstanceOf and asInstanceOf instead of pattern matching

name : **instance-of-used**
source : [InstanceOfUsed](/rules/extra/src/main/scala/com/lightbend/abide/extra/InstanceOfUsed.scala)

It is safer and more idiomatic to use pattern matching than to use isInstanceOf and asInstanceOf on objects