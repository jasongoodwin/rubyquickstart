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
Ruby is a dynamically typed language and allows mutability so it tends to be used in a very imperative style. It is worth noting that you should always try to prefer immutability but we will demonstrate changing out method `h` to take your name as a parameter and say hello to it/him/her.

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

With Ruby's dynamic typing, other types can be passed in to the method still with no ill effect:

```irb(main):036:0> h("Jason", "Goodwin")
Hello JasonGoodwin
=> nil```

Here we are demonstrating string contatenation. To demonstrate the expression that is being evaluated more clearly, we will ask the REPL to do it explicitly for us again:

```irb(main):037:0> "Jason"+"Goodwin"
=> "JasonGoodwin"```
