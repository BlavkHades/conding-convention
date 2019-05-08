Coding Conventions
=======================

This document is meant to serve as a guide to writing code in a codebase,
covering when and how to use various language features as well as how code
should be formatted. Our goal is to ensure a consistently high-quality codebase
that is easy to read and contribute to, especially for newcomers.

Codebase contains a wide variety of code from many different authors.
It's been through a few different major stages in its life, including stints in
multiple different repositories.  When in doubt about how to write or format
something, always prefer the advice here over existing conventions in the
code. If you're already touching some older code as part of your work, please
do clean it up as you go along. But please do not spend hours applying the
formatting guidelines here to code you aren't otherwise modifying. While we'd
love for the entire codebase to follow this guide, we'd rather get there
gradually than lose lots of git history and developer time to purely cosmetic
changes. That said, if cosmetic changes that you're making as part of a larger
diff keep growing in scope, it may be worth pulling them out into a separate
diff.

There's no well-defined cutoff here - just try to minimize effort for your
reviewers. A good rule of thumb is that if your cosmetic changes require adding
significant new sections to the diff (such as a function rename that touches
all callsites), it should probably be pulled out into its own diff.

### What to include ###

The golden rule for what to include/import is "include/import what you use" (IWYU). In brief,
this means you should not rely on any headers you include to transitively
include other headers which have definitions you require.

### Access control ###

Try to avoid the `protected` keyword. It tends to give a false sense of
security about encapsulation: since anyone can inherit from your class, anyone
can access the `protected` member with a little extra effort.

### Public data members vs. getters/setters ###

Prefer declaring public member variables to using getters and setters. Getters
and setters that don't manage object state in a nontrivial way serve to bloat
the API and introduce unnecessary boilerplate.

### Naming ###

## Components ##
It is recommended to write components name by its purpose. 
This approach improves the readability and maintainability of code.

## Classes ##
Usually class name should be noun starting with uppercase letter. 
If it contains multiple word than every inner word should start with uppercase.

Eg: String, StringBuffer, Dog

## Interfaces ##
Usually interface name should be adjective starting with uppercase letter. 
If it contains multiple word than every inner word should start with uppercase.

Eg: Runnable, Serializable, Comparable

## Methods
Usually method name should either be verb or verb noun combination starting with lower letter. 
If it contains multiple word than every inner word should start with uppercase.

Eg: print(), sleep(), setSalary()

## Variables ##
Usually variable name should be noun starting with lowercase letter. 
If it contains multiple word than every inner word should start with uppercase.

Eg: name, age. mobileNumber

if the variable save an array of any datatypes then the variable name should be pluralized.

Eg: names, ages, mobileNumbers

## Constants ##
Usually constant name should be noun. It should contain only uppercase If it contains 
multiple word than words are separated with ( _ ) underscore symbol. Usually we declare
constants with public static and final modifiers.