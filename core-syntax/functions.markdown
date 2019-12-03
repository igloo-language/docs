---
layout: default
title: Functions
nav_order: 3
parent: Core Syntax
permalink: /core_syntax/functions
---

# Functions
{: .d-inline-block }

Stable
{: .label .label-green }

Functions are a tidbit of code that run when they are called. They help make code more concise and readable. They take in values, and output values. In igloo, functions can be passed (required) positional arguments, **optional positional arguments**, and keyword arguments. Note: trailing commas are ok in Igloo.

# Function Declaration
Igloo uses the `func` keyword for function declarations. Creating a function is simple:

```
func my_func(pos_arg, pos_arg2, optional_arg?, keyword_arg=10) {
    // code
}
```

In the above code, everything looks quite normal, wit the positional arguments being named and having an identifier, and the keyword arguments having an equals sign denoting the default expression, with commas in between.

Something unusual you may have noticed is the use of the `?` after the optional argument...

# Optional Positional Arguments
In Igloo, optional positional arguments allow for some positional arguments not to be passed, and instead placed with the `null` type. Igloo reads the optional positional arguments after the required positional arguments. THis takes a while to get used to, but helps use to write better and easier to use libraries and functions:

```
func add(first_arg, second_arg, three?, four?){
    // Code here
}

add(11, 230, 10); // optional argument `three` is given the value of `10` and `four` a value of `null`
add(11, 230); // optional argument `three` and `four` are automatically given the value of `null`
add(11, 230, 12, 15); // optional argument `three` becomes `12` and `four` becomes `15`
```


