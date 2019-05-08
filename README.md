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

## General Convention ##

### Write comments and documentation ###

Perhaps one of the first things you learn as a developer is to comment your code. 
At first it may seem like a waste of time, 
following the mentality of ‘If they are a developer too – they can understand it’. 
While it is true some of the time, commenting your code and providing proper documentation 
will guide the other developers through the algorithm and logic that you implemented. 
But don’t get carried away and comment every line of code! Obvious code should be left as is.

### Write readable yet efficient code ###
Readable codes are easy to follow, yet use optimal space and time. 
When writing code you may often want to write it in as little lines as possible.
 Perhaps you can write an entire method or function in one line, 
 but that only makes it harder to read and understand.


### Use helper methods ###
It’s good practice to keep code concise and succinct. 
A method should only implement what it needs to do. 
If a part of your implementation does something else, 
put it in a separate method and call that within your method.

#### If avoidable, do NOT hard-code!
The only things that should be hard-coded are constants. That’s it.


### Write test cases.###
This way you know what your method does, what it takes and what it should return. 
You will know when it should work or when it should fail. 
A function should always be based on test cases; not tests on functions.

When creating APIs, writing Integration test that test all the behavior of an endpoint is of utmost importance



### Pair programming/code review ###
These are very helpful when it comes to refactoring your code. 
Others might see better implementation to optimize your code or just make your code more elegant. 
It also ensures that developers adhere to standards and the work is double checked. 
In addition to all that, it is a wonderful way for developers to learn from each other.

### BACKUP AND SAVE YOUR WORK OFTEN ###

Enough said. Dead battery, blackout, software glitch, fire, nuclear disaster – all of these may result in loss of data. Making sure you save often and back up your code on some kind of version control system is a simple way to ensure that your code stays safe.


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

## Naming ##

### Components ###
It is recommended to write components name by its purpose. 
This approach improves the readability and maintainability of code.

### Classes ###
Usually class name should be noun starting with uppercase letter. 
If it contains multiple word than every inner word should start with uppercase.

Eg: String, StringBuffer, Dog

### Interfaces ###
Usually interface name should be adjective starting with uppercase letter. 
If it contains multiple word than every inner word should start with uppercase.

Eg: Runnable, Serializable, Comparable

### Methods or Functions ###
Usually method name should either be verb or verb noun combination starting with lower letter. 
If it contains multiple word than every inner word should start with uppercase.

Eg: print(), sleep(), setSalary()

Each method name should state exactly what it does.

Eg: convertsIntegerToString(); solvesSimultaneousEquation(float a, float b, float c);

### Variables ###
Usually variable name should be noun starting with lowercase letter. 
If it contains multiple word than every inner word should start with uppercase.

Eg: name, age. mobileNumber

if the variable save an array of any datatypes then the variable name should be pluralized.

Eg: names, ages, mobileNumbers

### Constants ###
Usually constant name should be noun. It should contain only uppercase If it contains 
multiple word than words are separated with ( _ ) underscore symbol. Usually we declare
constants with public static and final modifiers.


### Namespaces ###

New namespaces should use `lowercase`---and single-word namespaces are greatly
prefered for common usage.  For longer namespaces (e.g., `vasm_detail`), use
`lower_case_with_underscores`.

## Formatting ##

While consistent code formatting doesn't directly affect correctness, it makes
it easier to read and maintain. For this reason, we've come up with a set of
guidelines about how code should be formatted. There's a good chance that some
of these will conflict with your own personal preferred style, but we believe
that having a consistently easy to read codebase is more important than letting
each developer write code that he or she thinks is uncompromisingly beautiful.

Anything not specified here is left up to the judgment of the developer.
However, this document is not set in stone, so if a particular formatting issue
keeps coming up in code review it probably deserves a few lines in here.

### General rules ###

- All indentation is to be done using spaces.
- Each indentation level is 2 spaces wide.
- Lines may be no longer than 80 characters, unless absolutely required for
  some syntactic reason.
- Lines should not have any trailing whitespace. This includes blank lines at
  non-zero indentation levels; the only character on those lines should be a
  newline.
- Opening braces go on the same line
  Eg:   if (true) {
            log(‘winning’);
        }

        if (true) {
            log(‘winning’);
        } else if (false) {
            log(‘this is good’);
        } else {
            log(‘finally’);
        }
- Declare one variable per var statement
  Eg: var keys = [‘foo’, ‘bar’];
      Integer values = 25;
      String value = "value";


### Method/Function ###
-   Write small functions: Keep your functions short. A good function fits on a slide 
    that the people in the last row of a big room can comfortably read.
-   Return early from functions: To avoid deep nesting of if-statements, 
    always return a function’s value as early as possible. 
    Right: 
        function isPercentage(val) {
            if (val < 0) {
                return false;
            }

            if (val > 100) {
                return false;
            }

            return true;
        }
    Wrong: 
        function isPercentage(val) {
            if (val >= 0) {
                if (val < 100) {
                return true;
                } else {
                return false;
                }
            } else {
                return false;
            }
        }
-   Method chaining: One method per line should be used if you want to chain methods.
    You should also indent these methods so it’s easier to tell they are part of the same chain.
    Eg: 
        User
            .findOne({ name: 'foo' })
            .populate('bar')
            .exec(function(err, user) {
               return true;
            });
### Comments ###
-   Comments: Use slashes for both single line and multi line comments.
    Try to write comments that explain higher level mechanisms or clarify difficult segments of your code. 
    Don’t use comments to restate trivial things.
    Eg:
        //this method handles the verification of a card transaction
        //this method triggers an event to update a users subscription...
        //if the transaction is successful
        exports.card = async  (req,res,next) => {

        }

### Code Commit ###
-   Commits should be done at the close of work each day and whenever you are through with a feature/bug-fix.
-   Always try to avoid to work on the master/release branch. 
    multiple people working on the master branch at the same time is a disaster waiting to happen.
-   Commit message should be descriptive and should discuss about the feature/bug-fix.

