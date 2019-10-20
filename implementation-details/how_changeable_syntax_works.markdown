There are 3 steps to running code as you know:

```
- lexing
- parsing
- interpreting
```

I'll go through this step by step.

`lexing` - it's the same as normal, and add extra rules when nessicary, using the `add_rule()` method (all is good)

`parsing` - this is the most complex part. When we parse some changeable syntax code (`impl`), add a parse time object that is global that affects all functions files and other namespaces/scopes (this is easy because parsing does not take into account scopes). As we find a rule we cannot parse we check the global parse time objects, and look for those. If one is that that matches, simply in the AST mark the name of the syntax used and all the data that is relevant to using it (e.g. names of variables used etc.). Again, don't worry about scopes in the parsing. When you run into an import statement, parse the file imported, then add every parse time object you find (in this case just `impl` statements). When you enter a function also parse it the `impl` blocks, and add the syntax rules to the global objects. *Again*, there are no scopes, which means that if an `impl` block is defined ther rule still exists in the parser even if it is deleted on the interpreter or in a different scope.

`interpreting` - when we run into an `impl` branch/node define it in the objects dictionary. The interpreter will already deal with scopes and variables so we do not need to worry about that. This is the magic part: as we run into a foreign node, lookup in the objects if the type of syntax exists, if it does GREAT! run the code in the `impl` block given as info from that specif syntax. If the syntax isn't defined in the objects, then raise an error.

One big problem there is that I don't know how to solve is say if there is a syntax in a function and one outside the interpreter would be messed up because the one in the function overwrite the one in the actual program.

For example:
```java
impl foo statement {}
func bar() { impl foo statement{} }
// foo statement
foo;
// it is parsed as the one in the function cause the parser does the most recent entry first
```
With the last line ^
