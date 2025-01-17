# Print, Puts, and Return

## Overview

We'll cover how the `puts` and `print`commands display Ruby code to the console, and then explain the concept of return values in Ruby.

## Objectives

1. Define and distinguish `puts` from `print`.
2. Identify implicit return values in Ruby syntax.
3. Distinguish between the display outputs of `puts` and `print`from their return values.
4. Use the explicit `return` keyword.


## `puts` and `print`

The `puts` (short for "out**put s**tring") and `print` commands are both used to display in the console the results of evaluating Ruby code. The primary difference between them is that `puts` adds a newline after executing, and `print` does not.

```ruby
3.times { print "Hello!" }
# > Hello!Hello!Hello!

3.times { puts "Hello!" }
# > Hello!
# > Hello!
# > Hello!
```

By default, Ruby doesn't display any output. The methods `puts` and `print` are a great way to explicitly tell the program to display specific information. Without these printing methods, Ruby will read the line, but not print anything out.

### Bonus: How Puts and Print put and print

How do the `puts` and `print` methods actually output text to your console? They use the `$stdout` global variable provided to us by Ruby. (You don't need to worry about writing global variables right now.) For the purposes of understanding how `puts` and `print` work, we just need to understand the following:

Your computer has a `$stdout` file that communicates with your operating system. So, `puts` and `print` actually send output to the `$stdout` variable. The `$stdout` variable sends that information to the `$stdout` file on your computer which then communicates with your operating system and then outputs that information to the console.

You can absolutely employ `puts` and `print` without understanding everything that was just described. But if you do understand it, then you now have a basic sense of what is happening under the hood of these methods.

## Returning Values

What methods like `puts` and `print` allows us to output to the console are different from Ruby's concept of a *return value*.

A return value is the data returned to the program by the execution of a method, the assignment of a variable, actually...

Everything in Ruby has a return value!

 For instance:

| Code                  | Return Value   |
|-----------------------|----------------|
| `"Hello world"`       | `"Hello world"`|
| `6 + 3`               | `9`            |
| `president = "Obama"` | `"Obama"`        |
| `total = 6 + 3`       | `9`            |
| `puts "hello world"`  | `nil`          |
| `print "hello world"` | `nil`          |


You may notice that the `puts` and `print` methods, when run in IRB, print values on the screen and then display a line like this: `=> nil`. This is because `puts` and `print` may print the value you want, but instead of *returning* that value, they return `nil`.

### Return Values of Methods

Methods are like vending machines. When you use a vending machine you just put in two arguments, the number (C7) and your money. We already know how to use arguments, but then your vending machine might do two thing. One, it will make a noise saying that everything worked, beep beep. Then it gives you the soda. The soda is the return type. But those beeps? Are you able to do anything with them? Nope! That's like puts: it just tells you stuff and then goes into the ether! Gone forever.

Every method in Ruby returns a value by default, even custom ones. This returned value will be the value of the last statement.

For example, let's look at this method called `restaurant`:

```ruby
def restaurant
  restaurant_name = "Guy's American Kitchen & Bar"
  cuisine = "american"
  motto = "Welcome to Flavor Town!"
end
```
The return value of the `restaurant` method is `"Welcome to Flavor Town!"` because that was the last statement evaluated.

Say you're the best chef in the world, Guy Fieri. To make a method that just prints your name and returns `nil`, you could write:

```ruby
def print_name
  puts "Guy Fieri"
end
```

To write a method that returns your name but doesn't print anything, you could write:

```ruby
def return_name
  "Guy Fieri"
end
```

To both print and return your name, you could write:

```ruby
def print_and_return_name
  puts "Guy Fieri"
  "Guy Fieri"
end
```
If you accidentally switched the order of the lines inside the method:

```ruby
def broken_print_and_return_name
  "Guy Fieri"
  puts "Guy Fieri"
end
```
The method would instead print "Guy Fieri" and return `nil`. This is because the last line that was evaluated was `puts ...` and the return value of a `puts`, as seen in the [table above](#returning-values) is always `nil`.

#### The Return Keyword

There is one other way to return a value from a method and that is to use the `return` keyword.

Let's take a look:

```ruby
def stylish_chef
  best_hairstyle = "Guy Fieri"
  return "Martha Stewart"
  "Guy Fieri"
end
```

What do you expect the return value of the above method to be? Go into IRB, copy and past the above method and call it. Go on, I'll wait.

...

You may have expected the return value to be "Guy Fieri". His name is the last line of the method and it is true that he does have the best style (you can't beat sunglasses on the back of the head, sorry).

*However*, the return value of the above method is actually `=> Martha Stewart`!

The return keyword will disrupt the execution of your method. If you employ it, your method will return whatever you have explicitly told it to (in this case, `"Martha Stewart"`), and terminate.

The explicit use of the `return` keyword is generally avoided by many Rubyists.

### Code Along Exercise: Practicing Return Values

Let's try it out once more together. In your terminal, drop into IRB. Then, follow the steps below:

1. In IRB, type: `6 + 3`
  * You should see a return value of `=> 9`

2. Now, set a variable `total` equal to `6 + 3`.
  * You've just *stored* the return value of adding `6` and `3` and you can now grab that return value `9` by referencing the `total` variable.
3. Set another variable, `new_total` equal to `total + 10`.
  * You should see a return value of `19`.
4. Copy and paste the below method definition in IRB, then invoke the method with an argument of `"Johnny"`.

```ruby
def the_shining(name)
  puts "Here's #{name}!"
end
```
You should see the following output:

```
Here's Johnny!
=> nil
```

First, the method output the phrase to the terminal, then the terminal displayed the return value for us, which is `nil` (the return value of the `puts` method!)

### Why Return Values Matter

Return values are how different parts of your program communicate with one another. You don't have to worry too much about this for now, but as you start to build more complicated programs, you'll find that the return value of one method might be operated on by a subsequent method.

Let's look at a very basic example. Earlier, in IRB, we set a variable `total` equal to the return value of adding `6 + 3`. If you've left IRB, drop back in and re-create your `total` variable as the sum of `6 + 3`.

On the next line, execute `total + 17`. You should see a return value of `=> 26`. Thus, the return value of one operation (`6 + 3`) was used to execute further operations (the addition of `17`).

As we've just done, you'll find that we will often store return values in variables so that we can use them later.
