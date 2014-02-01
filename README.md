rubyquickstart
==============

A sing-along document showing you Ruby in 20 minutes. This is for experienced programmers who want a fast ramp up.
This is based heavily on the document found here: https://www.ruby-lang.org/en/documentation/quickstart/
No time will be wasted explaining concepts that you likely know if you're a fairly experienced programmer.
Setup is assumed complete of ruby and irb - they come pre-installed on OSX so many of you won't have to worry.

Warning
=======
I'm learning Ruby while writing this so it may not be complete or 100% correct. I'll revisit the document to make corrections about assumptions and update this section of the document with the corresponding confidence level I have in the correctness.

REPL/IRB
========
We'll be working through the basics through the REPL (read-eval-print-loop) as it's the best way to get quick feedback on experimentation while learning a language.
To start the REPL, open a terminal and type `irb`
You'll now be at the Ruby REPL aka the "Interactive Ruby Shell"

Everything is an Expression
===========================
Ruby expressions return values. This is demonstratable by typing some different expressions in the REPL and seeing that there is a returned object from the expression. Unlike some other REPLs (eg Scala), the result of expressions are not assigned to an addressible variable name.

```irb(main):001:0> "Hello world"
=> "Hello world"
irb(main):002:0> 3 + 5
=> 8```

In order to assign the results of expressions, we have to start creating object references.
```irb(main):004:0> first_message="Hello World"
=> "Hello World"
irb(main):005:0> puts first_message
Hello World
=> nil```

Arity-1 Infix Notation
================
You may have noticed that I used infix notation on the arity 1 method puts. This is an optional syntax for arity-1 methods. Ruby method parameters are more often passed in braces. As far as I'm aware, there are no style guidelines around which notation to use.
```irb(main):009:0> Math.sqrt(4)
=> 2.0```

Defining a Method
=================
Ruby likes to forego the C-style curly braces and use plain english to fit into a more natural reading flow. Various keywords represent the opening of an expression and `end` generally represents the closing of the expression in the places of good old c style {}. We can start to see this now that we are ready to define a method with the def and end keyword pairing. (note: we'll start to forego the repl feedback on some of the examples now that you have been introduced.)

```def h
  puts "Hello world"
end```

Now we have our first method defined! We can call that method now:
```irb(main):026:0> h
Hello world
=> nil```

Dynamic Typing
==============
Ruby's type system is dynamically typed and strongly typed. What this means is that Ruby will not check type compatability at compile time so you can assign an int to a value that was created as a string. It is still strongly typed object-oriented language meaning that there ARE types in the language - a string is a string and a number is a number so you can't add "3" and 3 without converting the string into a numeric type unlike perl which can allow you to treat strings and numbers interchangably. It's probably worth noting that the terms ('dynamically typed/statically typed' and 'weakly typed/strongly typed') do not have precise definitions but are still useful concepts for describing a language's stance on typing.   

```def h(name)
puts "Hello #{name}"
end```

Now h has a new reference method (demonstrating string interpolation to boot) and we can call it to have our cute little computer say hi to us!

```irb(main):031:0> h "jason"
Hello jason
=> nil```

String Interpolation
====================
It's probably worth mentioning here that string intepolation contains expressions NOT simply variable names. For example, let's change our h reference to a new method:

```def h(val1, val2)
puts "Hello #{val1 + val2}"
end```

And if we evoke it, we can expect that expression to be evaluated as any other ruby expression:
```irb(main):035:0> h(1, 2)
Hello 3
=> nil```

Note that there is an implicit conversion happening there to change the numeric data type into a string to print. You don't have to worry too much about the types which is the double-edged sword that comes with more dynamically typed languages. 

With Ruby's dynamic typing, other types can be passed in to the method still with no ill effect. Strings would be an obvious choice to try in this case:

```irb(main):036:0> h("Jason", "Goodwin")
Hello JasonGoodwin
=> nil```

Here we are demonstrating string contatenation. To demonstrate the expression that is being evaluated more clearly, we will ask the REPL to do it explicitly for us again:

```irb(main):037:0> "Jason"+"Goodwin"
=> "JasonGoodwin"```

Making Parameters Optional
==========================
Now that we've looked at methods a bit, lets look at how me might start defining an API with optional fields. Lets have our method h print a name and an optional last name. Because Smith is the most common last name in Australia, I can make an assumption that a last name is Smith if it's not provided so let's go with that:

```def h(first, last = "Smith")
puts("Hello #{first} #{last}")
end```

Now if we're desigining a name printing API to open source and share with the world, we can make last name optional and make a reasonably safe assumption that a person's last name is "Smith"! We are already making the world a better place.

Getting Functional
==================
 Ruby is a multi-paradigm language and does have many functional characteristics. Functions are first class citizens meaning that functions can be treated like other variables and be passed into other functions. For the below example, we will demonstrate this by defining a function and passing it into a second function and then it will be invoked. There are a couple ways to demonstrate this - in this case we will use what is referred to as a method object. 
 
 First, let's define an arity1 function that we will pass as a variable later later:

```def arity1(param)
puts("The arity1 method param is: #{param}")
end```

Now let's take a second method that has a parameter of the Method object type - the method object has a call parameter that will execute the method.

```def funky_method_executor(funky_method)
funky_method.call("FUNKY") 
end```

In the above you can see we are passing in the Method object like any other. 
Now let's try to compose the methods so we are passing the method arity1 into funky_method_executor as its parameter. In order to do this, we have to use `method` to aquire the method object for the method. 

```funky_method_executor(method(:arity1))
```
Now that we called the method `method` to get the method object we needed to use as an argument. The `:` infront of the method name is used in ruby to represent a symbol - remember almost everything is an expression in Ruby so if you don't use the colon, ruby will try to execute the method instead of passing the method in. Because the method requires a parameter, this will cause an exception to occur like so:

```irb(main):035:0> funky_method_executor(method(arity1))
ArgumentError: wrong number of arguments (0 for 1)
	from (irb):20:in `arity1'
	from (irb):35
	from /usr/bin/irb:12:in `<main>'```

Getting Object Oriented
=======================
Ruby land is a world full of nouns - it is a pure Object Oriented language meaning that everything in Ruby is an object. This allows us to draw on all of the world's learnings on object oriented programming including subjects such as design patterns and refactoring definitions as described by Martin Fowler in his book on Refactoring. In fact, there is a 'port' of refactoring for Ruby (see: http://www.amazon.com/Refactoring-Edition-Addison-Wesley-Professional-Series/dp/0321984137)

While Ruby is a pure object oriented language, there is a fairly strong deviation in how OO 'works' due to the dynamic type. Compared to, say, Java, there is no 'interface' in the language because types are never checked (i.e. no type-safety). Instead, object oriented languages with dynamic type systems talk about 'duck typing' which means that, instead of interfaces, objects use methods and arguments to determine valid semantics (citation: http://en.wikipedia.org/wiki/Duck_typing). In the end, this does mean that you will tend to lean more on tests than the compiler to ensure correctness in code. Refactoring cannot be done with confidence without good testing in place first.






Style
=====
(In progress - notes)
- 2 space indentation
- Comments are a smell
- Camels for Classes, Snakes Everywhere Else. Constants there is devision on (camelcase or uppercase snake)
- Generally Rubyists use parenthesis on arity1+ methods. Don't use parenthesis on arity0 methods. No parenthesis on if statements etc.
- Blocks - if it's small, fold into a line and use parenthesis. Multi statement use multiple lines do/end.

TODO
====
- Rebase history and force push 
- Discuss parenthesis style preference for arity0/1 methods. Also Arity 2+ methods DON'T require parenthesis
