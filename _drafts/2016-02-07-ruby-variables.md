---
layout: post
title: Getting Hold On Ruby Variables!
date: 2016-01-01
comments: true
---

Ever wondered what is the job of a variable is? Its simple, they point to objects in memory.
<!-- In Ruby objects exist in arbitrary memory locations. The dynamic nature of modern computing implies the need for a way to refer to specific objects in memory without having to keep track of their specific memory locations. This is the job of a variable, to point to objects in memory. -->

So how does ruby do it?
Ruby maintains tables of known variables and their values for each lexical scope and instance referred to as bindings. Once you start using a variable, Ruby simply creates a new entry in one of these tables. However, that first variable access must be an assignment or Ruby will throw a NameError: undefined local variable or method exception.

<!-- There are several types of variables in Ruby. Though each is used in its own way, they generally follow the same patterns. They're all dynamically typed named storage for objects that are accessible at varying scopes and (for the most part) must be assigned to before read. There are some intricacies at play here, but for the most part the common uses of local and instance variables come with no surprises. -->

There are 6 types of Variables in ruby:

* **Local Variables** - Typically the most common type of variable. Local variables exist within specific lexical scopes, and go "out of scope" when that scope ends.

* **Instance Variables** - These exist within the context of an instance. Each instance of a class will have its own specific set of these variables, independent from other instances of the same class.

* **Class Variables** - These exist at the class level, and are accessible from the class scope (inside the class, but outside of any methods) and within class methods.

* **Class Instance Variables** - Prefer class instance variables over class variables when you do really need store data at a class level. Class instance variables use the same notation as that of an instance variable. But unlike instance variables, you declare them inside the class definition directly.

* **Global Variables** - These are rarely used as they break the rules of encapsulation. However, Ruby supports them and they are used in a few places.

* **Constants** - Constants can be similar to both local and class variables in their scope, and can only be assigned to once (though there are workarounds). They also have a surprising use in how the class hierarchy is implemented.

The first character of an identifier categorizes it at a glance:

$	global variable
@	instance variable
[a-z] or _	local variable
[A-Z]	constant
The only exceptions to the above are ruby's pseudo-variables: self, which always refers to the currently executing object, and nil, which is the meaningless value assigned to uninitialized variables. Both are named as if they are local variables, but self is a global variable maintained by the interpreter, and nil is really a constant. As these are the only two exceptions, they don't confuse things too much.

You may not assign values to self or nil. main, as a value of self, refers to the top-level objec
