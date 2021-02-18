# Introduction

Hello and welcome to my book on Haskell, the functional programming language.  In this book you will learn the basics of the language, data structures, algorithms,  game development, statistics, probability, calculus, proofs, linear algebra, abstract algebra, topology, category theory, erogodic theory and machine learning.  

## The Road Ahead - Table of Contents

* Installation
* Haskell basics
* Data Structures
* Algorithms
* Probability
* Calculus
* Linear Algebra
* Proofs
* Statistics
* Topology
* Machine Learning
* Abstract Algebra
* Category Theory
* Erogodic Theory
* Game Development

Why these set of topics?  Well because along with each topic we learn, we'll see how to make use of it in Haskell.  The reason we are including Data Structures and Algorithms should be obvious - because it's what most undergraduates learn first.  We need to write something and it needs to be relatively straight forward.  We'll see that implementing algorithms and data structures are exceedingly simple compared to object oriented languages.  However, this assumes the concepts are already clear in your head.  I've decided to include probability and statistics mostly so we have something else relatively straight forward to implement.  Machine learning is included to motivate linear algebra, which we will need for abstract algebra.  The inclusion of proofs, abstract algebra, topology and erogodic theory is included to motivate category theory.  Category theory occurs throughout Haskell, so we need it, not just for theoretical purposes, but to be of actual use.  Finally, we include game development to tie together the applied mathematics and the applied computer science.  We'll make use of algorithms, data structures and machine learning in order to "do" game development.  Additionally, this topic is included because a lot of folks want to learn programming just for this reason.  As a secondary justification, much of the early machine learning was done in conjunction with artificial intelligence in the gaming context.  For the interested reader, I recommend checking out Arth Samuel's work on the subject.  

## Installation

Before we get started with any of this though, we'll need a way to execute haskell programs.  For that we'll need two programs:

* ghc - the haskell interpretter and compiler
* ghci - the interactive haskell repl

We can install them easily on Ubuntu:

`sudo apt install ghc`

## Haskell Basics

The basics of haskell look much like many other modern languages.  We can do basic mathematics:

Addition:

```haskell
5 + 7
```

Multiplication:

```haskell
50 * 74
```

Division:

```haskell
5 / 2
```

We can do basic logic:

The AND operator is `&&` like so:

```haskell
True && False
```

The OR operator is `||` like so:

```haskell
False || True
```

And the NOT operator is `not` like so:

```haskell
not False
```

We can use numbers to generate logical statements:

We can check that two numbers are equal:

```haskell
5 == 5
```

We can also check if two numbers are unequal:

```haskell
4 /= 5
```

We can even do this with strings:

```haskell
"hello" == "hello"
```

### Functions in Haskell

Up until now we've been looking at code that more or less "feels" like other languages.  With some minor exceptions, you probably won't be sure if you were writing Haskell or Java or Python.  But now the differences will become very stark.  Haskell is a "functional" language, which means everything is "about" the function.  

Let's look at some built in functions first:

```haskell
succ 8
```

this function is called a successor function and it takes in a single number and increments the number by one.  Not very exciting, but you should notice some pretty big differences from languages like Python, Java or really anything else you've seen before.  The biggest difference is the absence of parentheses, they look like this: `()`.  I personally have very strong mixed feelings about this, but it's a choice of the language for a reason that will become apparent later on.

The function we just saw is called a prefix function.  This is because of how the function gets used in the program.  It's called "prefix" because the function comes before the parameters.  We've actually already been using a class of functions called "infix" functions, called as such because they occur in-between the parameters.

Let's look at a second example of a built in prefix function in haskell, this time with two parameters:

```haskell
min 9 10
```

As you can see this one takes in two parameters, in this case 9 and 10.  You might be thinking, how would I read a set of functions together?  How do I know when one function ends and the next one begins.  Well, this is where parentheses come back into the picture:

```haskell
(succ 9) + (min 12 15)
```

Here we use parentheses to separate the parameters of the two functions.  What can upset some people coming from other languages, including me is that the following is also valid:

```haskell
succ 9 + min 12 15
```

the reason you can "even" do this is because of the infix functions separating the two prefix functions.  But please don't do it.  It's just "wrong".

One final note before we write our first function.  We can call functions on the results of other functions like so:

```haskell
succ (succ 9)
```

The result of this would be 11 because we add 1 to 9 and then 1 to 10 (the result of 9 + 1).  

### Our first function

```haskell
timesTwo x = x * 2
```

This simple function takes in a single parameter `x` and then returns x * 2.  So if we passed in `2`, the function would `4`.

Some things to notice about how this function was defined:

* functions do not require special keywords to be defined.
* function parameters are specified first
* the function's definition is specified by everything on the right hand side of the equals sign.

This kind of function definition lends itself to short functions, ideally ones that can be written on a single line.  Of course, you'll still need glue functions to tie everything together.  But ideally, your code is decomposed into as many component pieces as possible, and then functions are strung together for readability.

In addition to being able to use a function in prefix, we can also call any function we might like as infix.  For instance, let's define a division function:

```haskell
division x y = x/y
```

To use this function as an infix we simply do:

```haskell
5 `division` 7
```

We need to specify the backticks in order to use our function as an infix.

## Flow of Control

Now that we've seen how to make simple functions, let's look at a function that allows for flow of control:

```haskell
scaleDownLargeNumbers x = if x > 100 
						  then x/10
						  else x
```

As you can see all flow of control statements require an if AND an else.  That's because functions in haskell _must_ return something.  Also notice the general syntax:

```
if [conditional] 
then [result-if] 
else [result-else]
```

Let's say we wanted a second implementation of the function that did something slightly different but followed a similar idea.  Then we would do:

```haskell
scaleDownLargeNumbers' x = if x > 1000 
						   then x/10
						   else x
```

In this case, the function name is said "scaled down large numbers prime".  The `'`' indicates the "prime".  This is typical notation from calculus and is borrowed here in haskell.

Notice, the function definition is generally the same, and is only off by an order of magnitude.  This convention helps us to work with sets of similar ideas while keeping individual function definitions small.  We'll see this notation aid us directly when we talk about calculus.

## Variables

Like in other languages, we can define variables in Haskell, although they are of less value than functions, seeing as how this is a "functional" language.

```haskell
let x = 7
```

Here we have defined x and bound the value of `7` to it.  There is actually quiet a bit more it than that, but a detailed introduction is out of scope for now.  When we get into advanced language syntax, we will discuss more about variable binding.  For now, just treat this as the way to do variable assignment.

## Collections 

Now that we have a notion of variable binding, we can introduction collections.  We'll start with the built-in collections.  Since a list is just a collection of variables, let's start with that.  The syntax should look familar from other languages:

```haskell
let numberList = [1,2,3,4,5,6]
```

We can concatenate lists together with the `++` function.

```haskell
let listOne = [1,2,3]
let listTwo = [4,5,6]
let listThree = listOne ++ listTwo
```

Here `listThree` is the concatenation of the first two lists and they will be concatenated from left to right.  Note: that if the first list is very large then it can take a while to concatenate the two lists.  For this reason, Haskell also implements single element prepend operator.

The prepend operator looks like this:

```haskell
let list = [1,2,3]
let newList = 0:list
```

Here the new list will be:

```haskell
[0,1,2,3]
```

We can also compare lists in a few ways.  All of the following infix functions are legitimate:

* <
* >
* <= 
* >=
* ==

The inequalities compare element by element with by index, so if we had the following:

```haskell
let a = [1,2,3]
let b = [2,1,4]
a < b
```

The statement `a < b` would be True.  Because at index zero for both lists the following holds:

```
a[0] < b[0]
```

If a[0] == b[0], then a[1] and b[1] are compared.  And so on and so forth.  This is useful as a primative for sorting lists, which we will make use of later.

The last boolean function, `==` checks to see if all the elements are the same.

So,

```haskell
let a = [1,2,3]
let b = [1,2,4]
a == b
```

Would return False, but

```haskell
let a = [1,2,3]
let b = [1,2,3]
a == b
```

Would return True.

There is also a nice function syntax for generating ranges:

```haskell
let a = [1..1000]
```

The above generates a list with the numbers 1 to 1000 inclusive, so the first element is 1 and the last element is 1000.  This is a departure from other languages and should be accounted for.

In addition to being able to specify an integer pattern, one can also supply another obvious pattern like:

```haskell
let a = [0.1, 0.2, 0.3 .. 1]
```

And haskell will take care of the rest.  The resultant list is:

```
[
	0.1,
	0.2,
	0.30000000000000004,
	0.4000000000000001,
	0.5000000000000001,
	0.6000000000000001,
	0.7000000000000001,
	0.8,
	0.9,
	1.0
]
```

As you can see it's not exactly right.  In addition, you can also specify increasing sequences that aren't just increasing by some unit amount:

```haskell
let a = [0.1, 0.3 .. 1]
```

Will produce:

```
[
	0.1,
	0.3,
	0.5,
	0.7,
	0.8999999999999999,
	1.0999999999999999
]
```

Pretty neat right!

There are also a number of other assorted standard operators:

* length:

```haskell
let xs = [1,2,3,4,5,5]
length xs
```

This will return the size of the list.

* reverse:

```haskell
let xs = [1,2,3,4,5,5]
reverse xs
```

This will reverse the elements of the list.  In this case the result will be:

```haskell
[5,5,4,3,2,1]
```

* index

```haskell
let xs = [1,2,3]
xs !! 2
```

This will get the 3rd element of the list, because lists are indexed starting at zero.  In general the pattern:

```
list !! [index]
```

Returns the nth 'index' of the list.  Note: the last recoverable element is 

`[length of list] - 1`

Because the list starts are index `0` and goes to index `n-1`, where `n` is the length of the list.

* filter

```haskell
let xs = [1,2,3,4,5,6]
myFilter x = if x > 3 then True else False 
filter myFilter xs
```

Here the filter takes in a specific predicate, in otherwords another function as it's first argument and a list as it's second.  Then a "filtered" version of the list is returned.  In this case, the returned list is:

```
[4,5,6]
```

Because those are the elements for which the filter predicate return `True`.  

I chose to write the above filter in a syntax that would be familiar based on what we've seen thus far.  Typically it is far cleaner to write your filter predicates as unnamed predicates if the condition is simple enough.  Let's see an example of the same piece of code, but cleaned up:

```haskell
let xs = [1,2,3,4,5,6]
filter (>3) xs
```

Here we don't specify a variable, but rather just the condition to check.  It feels a little bit sloppy that the language implements the predicate first, but we can easily change that by implementing our own filter:

```haskell
let xs = [1,2,3,4,5,6]
let ourFilter list predicate = filter predicate list
ourFilter xs (>3)
```

Now this reads like english:

filter our list, xs, to only those elements greater than 3.  

null:

```haskell
null []
```

This checks if the list is the empty list, defined as `[]`.  So anything other than passing `[]` to null returns `False`.  Note the code presented above returns `True`.

any:

```haskell
let xs = [1,2,3,4,5]
any (>3) xs
```

The any keyword checks to see if the condition is ever true in the list.  In this case it will return `True` because there are elements larger than `3` in the list.  The general syntax is:

`any [predicate function] [list of elements]`

all:

```haskell
let xs = [10, 11, 12 13]
all (>5) xs
```

The all keyword checks to see if the condition is true for _all_ the elements in the list.  In this case it will return `True` because all the elements are greater than `5`.  The general syntax is the same as the any function:

`all [predicate function] [list of elements]`

Here is an example that will return false:

```haskell
let xs = [1,2,3]
all (>2) xs
```

This fails because not all of the elements are greater than `2`, namely the first two elements are less than or equal to `2`.

map:

```haskell
let xs = [1,2,3]
map (*2) xs
```

Here the resultant list will be:

```
[2,4,6]
```

In general the map function applies a predicate, another function, to each element of the list.  Here we are multiplying by two.  In general, any predicate can be applied to a list of elements.

elem:

```haskell
let xs = [1,2,3]
3 `elem` xs
```

Here the elem function will be `True`.  In general elem checks for membership in a list.  So we are asking the question is 3 in the list, xs?

In general the syntax looks like:

```
[element to check for] `elem` [list of elements]
```

splitAt:

```haskell
let a = [1,2,3,4,5]
let (one, two) = splitAt 2 a
two
```

The splitAt function splits a list into two parts starting at the index supplied.  In this case this code would return `[3,4,5]`.  I leave it as an exercise to figure out what the list named one contains.

In general the syntax is:

```
splitAt [index to split at] [list of elements]
```

## List Comprehensions

Like many other languages Haskell comes with a list comprehension.  Let's look at a simple example to start:

```haskell
let a = [1..10]
[x | x <- a]
```

This trivial example just reproduces the first list.  But it highlights part of the syntax:

```
[[transformation goes here] | [variable] <- [list to iterate over]]
```

Now let's look at a slightly non-trivial example:

```haskell
let a = [1..10]
let b = [x*2 | x <- a]
```

The values in b will be:

```
[2,4,6,8,10,12,14,16,18,20]
```

As you can see we applied the mapping `x*2` to each element in a.  We can clean up the syntax a little by bringing the iteration into the comprehension:

```haskell
let b = [x*2 | x <- [1..10]]
```

Now let's add a flow of control step.  Say we only want to keep odd numbers and we still want to multiply those numbers by two:

```haskell
let a = [x*2 | x <- [1..10], x `mod` 2 == 1]
```

This returns:

```
[2,6,10,14,18]
```

This new segment occurs after the iteration and must return a boolean.  Trivially, if we wanted our sequence to be empty we could do this:

```haskell
let a = [x*2 | x <- [1..10], False]
```

This returns:

`[]`

That is because False is _always_ False.  So nothing in the list gets processed.  We could also set this condition to True and then the additional part of the list comprehension would have no effect.  
We are not limited by including only one predicate, we can infact include as many as we like:

```haskell
let a = [x*2 | x <- [1..10], x /= 8, x /= 7, x /= 4]
```

This returns:

```
[2,4,6,10,12,18,20]
```

Finally, we can also include flow of control in the transformation step:

```haskell
let a = [if x < 5 then x*2 else x*3 | x <- [1..10]]
```

This returns:

```
[2,4,6,8,15,18,21,24,27,30]
```

Now that we have all the components of a list comprehension, it should be noted that we need not restrict ourselves to single lists.  Anything we can do with one list, we can do with two:

```haskell
let a = [1..3]
let b = [4..6]
let c = [x*y | x <- a, y <- b]
```

Here c equals be:

```
[4,5,6,8,10,12,12,15,18]
```

This will be one of those "large" departures from what typically happens in list comprehensions.  Instead of iterating over both lists index by index, which is what one might expect coming from Python or Java, Haskell does something all together different.  Instead, Haskell will multiply _every_ pair of elements in our finite range.  If we were to write this in Python it would look something like this:

```python
import itertools

a = [1,2,3]
b = [4,5,6]
c = sorted([
    elem[0]*elem[1]
    for elem in itertools.product(a, b)
])
```
