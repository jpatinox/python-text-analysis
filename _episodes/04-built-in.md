---
title: "Built-in Functions and Help"
teaching: 15
exercises: 10
questions:
- "How can I use built-in functions?"
- "How can I find out what they do?"
- "What kind of errors can occur in programs?"
objectives:
- "Explain the purpose of functions."
- "Correctly call built-in Python functions."
- "Correctly nest calls to built-in functions."
- "Use help to display documentation for built-in functions."
- "Correctly describe situations in which SyntaxError and NameError occur."
keypoints:
- "Use comments to add documentation to programs."
- "A function may take zero or more arguments."
- "Commonly-used built-in functions include split(), join(), upper(), lower(), replace(), startswith()."
- "Functions may only work for certain (combinations of) arguments."
- "Functions may have default values for some arguments."
- "Use the built-in function `help` to get help for a function."
- "The Jupyter Notebook has two ways to get help."
- "Every function returns something."
- "Python reports a syntax error when it can't understand the source of a program."
- "Python reports a runtime error when something goes wrong while a program is executing."
- "Fix syntax errors by reading the source code, and runtime errors by tracing the program's execution."
---
## Use comments to add documentation to programs.

~~~
# This sentence isn't executed by Python.
favoritePet = "Dog"   # Neither is this - anything after '#' is ignored.
~~~
{: .language-python}

## A function may take zero or more arguments.

*   We have seen some functions already --- now let's take a closer look.
*   An *argument* is a value passed into a function.
*   `len` takes exactly one.
*   `int`, `str`, and `float` create a new value from an existing one.
*   `print` takes zero or more.
*   `print` with no arguments prints a blank line.
    *   Must always use parentheses, even if they're empty,
        so that Python knows a function is being called.

~~~
print('before')
print()
print('after')
~~~
{: .language-python}
~~~
before

after
~~~
{: .output}

## Commonly-used built-in methods include `split`, `join`, `upper`, `lower`, `replace`, `startswith`.
### `upper` and `lower` methods

*   Use `upper` method to return a copy of a string converted to upper case.
*   Use `lower` method to return a copy of a string converted to lower case. 

~~~
first_name = “Ahmed”
print(first_name.upper())
~~~
{: .language-python}
~~~
AHMED
~~~
{: .output}

*Note:  The `upper` method example above did not modify the original string.  Instead, it created a copy of the original string.  This is because strings are considered immutable data types, meaning they cannot be changed after creation.  When you run a method on a string, a brand new string is created and the original remains unchanged.
~~~
first_name = “Ahmed”
print(first_name.lower())
~~~
{: .language-python}
~~~
ahmed
~~~
{: .output}

### `split` and `join` methods
*   Use `split` method to split a string into a list where each word is a list item
*   Use `join` to method to take all items in an iterable object (i.e. objects capable of returning its members one at a time, such as a list) made up of strings and join them into one string.  
~~~
name = “Big Bird”
print(name.split())
~~~
{: .language-python}
~~~
[‘Big’, ‘Bird’]
~~~
{: .output}
~~~
pets = [‘bunny’, ‘cat’, ‘dog’]
print(‘+’.join(pets))
~~~
{: .language-python}
~~~
bunny+cat+dog

~~~
{: .output}

* The string whose method is called (‘+’ in this example) is inserted in between each given string (passed via parameter). The result is returned as a new string.

### `replace` and `startswith` methods
*   Use `replace` to return a copy of a string where a specified value is replaced with a specified value
*   Use `startswith` to returns true if the string starts with the specified value
~~~
pet = “I like cats”

newPet = pet.replace(“cats”, “dogs”)

print(pet)

print(newPet)
~~~
{: .language-python}
~~~
I like cats
I like dogs

~~~
{: .output}

*Note:  all occurrences of the specified phrase will be replaced , if nothing else is specified.
~~~
species = “Cats are not dogs”

x = species.startswith(“Cats”)

print(x)

~~~
{: .language-python}
~~~
True

~~~

*The specified value must match exactly and is case sensitive.



## Functions may only work for certain (combinations of) arguments.

*   `max` and `min` must be given at least one argument.
    *   "Largest of the empty set" is a meaningless question.
*   And they must be given things that can meaningfully be compared.

~~~
print(max(1, 'a'))
~~~
{: .language-python}
~~~
TypeError                                 Traceback (most recent call last)
<ipython-input-52-3f049acf3762> in <module>
----> 1 print(max(1, 'a'))

TypeError: '>' not supported between instances of 'str' and 'int'
~~~
{: .error}

## Functions may have default values for some arguments.

*   `round` will round off a floating-point number.
*   By default, rounds to zero decimal places.

~~~
round(3.712)
~~~
{: .language-python}
~~~
4
~~~
{: .output}

*   We can specify the number of decimal places we want.

~~~
round(3.712, 1)
~~~
{: .language-python}
~~~
3.7
~~~
{: .output}

## Use the built-in function `help` to get help for a function.

*   Every built-in function has online documentation.

~~~
help(round)
~~~
{: .language-python}
~~~
Help on built-in function round in module builtins:

round(number, ndigits=None)
    Round a number to a given precision in decimal digits.
    
    The return value is an integer if ndigits is omitted or None.  Otherwise
    the return value has the same type as the number.  ndigits may be negative.
~~~
{: .output}

## Python reports a syntax error when it can't understand the source of a program.

*   Won't even try to run the program if it can't be parsed.

~~~
# Forgot to close the quote marks around the string.
name = 'Feng
~~~
{: .language-python}
~~~
  File "<ipython-input-56-f42768451d55>", line 2
    name = 'Feng
                ^
SyntaxError: EOL while scanning string literal
~~~
{: .error}

~~~
# An extra '=' in the assignment.
age = = 52
~~~
{: .language-python}
~~~
  File "<ipython-input-57-ccc3df3cf902>", line 2
    age = = 52
          ^
SyntaxError: invalid syntax
~~~
{: .error}

*   Look more closely at the error message:

~~~
print("hello world"
~~~
{: .language-python}
~~~
  File "<ipython-input-6-d1cc229bf815>", line 1
    print ("hello world"
                        ^
SyntaxError: unexpected EOF while parsing
~~~
{: .error}

*   The message indicates a problem on first line of the input ("line 1").
    *   In this case the "ipython-input" section of the file name tells us that
        we are working with input into IPython,
        the Python interpreter used by the Jupyter Notebook.
*   The `-6-` part of the filename indicates that
    the error occurred in cell 6 of our Notebook.
*   Next is the problematic line of code,
    indicating the problem with a `^` pointer.

## <a name='runtime-error'></a> Python reports a runtime error when something goes wrong while a program is executing.

~~~
age = 53
remaining = 100 - aege # mis-spelled 'age'
~~~
{: .language-python}
~~~
NameError                                 Traceback (most recent call last)
<ipython-input-59-1214fb6c55fc> in <module>
      1 age = 53
----> 2 remaining = 100 - aege # mis-spelled 'age'

NameError: name 'aege' is not defined
~~~
{: .error}

*   Fix syntax errors by reading the source and runtime errors by tracing execution.

## The Jupyter Notebook has two ways to get help.

*   Place the cursor anywhere in the function invocation 
    (i.e., the function name or its parameters),
    hold down `shift`,
    and press `tab`.
*   Or type a function name with a question mark after it.

## Every function returns something.

*   Every function call produces some result.
*   If the function doesn't have a useful result to return,
    it usually returns the special value `None`.

~~~
result = print('example')
print('result of print is', result)
~~~
{: .language-python}
~~~
example
result of print is None
~~~
{: .output}

> ## What Happens When
>
> 1. Explain in simple terms the order of operations in the following program:
>    when does the addition happen, when does the subtraction happen,
>    when is each function called, etc.
> 2. What is the final value of `radiance`?
>
> ~~~
> radiance = 1.0
> radiance = max(2.1, 2.0 + min(radiance, 1.1 * radiance - 0.5))
> ~~~
> {: .language-python}
> > ## Solution
> > 1.
> >    1. `1.1 * radiance = 1.1`
> >    2. `1.1 - 0.5 = 0.6`
> >    3. `min(radiance, 0.6) = 0.6`
> >    4. `2.0 + 0.6 = 2.6`
> >    5. `max(2.1, 2.6) = 2.6`
> > 2. At the end, `radiance = 2.6`
> {: .solution}
{: .challenge}

> ## Spot the Difference
>
> 1. Predict what each of the `print` statements in the program below will print.
> 2. Does `max(len(rich), poor)` run or produce an error message?
>    If it runs, does its result make any sense?
>
> ~~~
> easy_string = "abc"
> print(max(easy_string))
> rich = "gold"
> poor = "tin"
> print(max(rich, poor))
> print(max(len(rich), len(poor)))
> ~~~
> {: .language-python}
> > ## Solution
> > ~~~
> > print(max(easy_string))
> > ~~~
> > {: .language-python}
> > ~~~
> > c
> > ~~~
> > {: .output}
> > ~~~
> > print(max(rich, poor))
> > ~~~
> > {: .language-python}
> > ~~~
> > tin
> > ~~~
> > {: .output}
> > ~~~
> > print(max(len(rich), len(poor)))
> > ~~~
> > {: .language-python}
> > ~~~
> > 4
> > ~~~
> > {: .output}
> > `max(len(rich), poor)` throws a TypeError. This turns into `max(4, 'tin')` and 
> > as we discussed earlier a string and integer cannot meaningfully be compared.
> > ~~~
> > TypeError                                 Traceback (most recent call last)
> > <ipython-input-65-bc82ad05177a> in <module>
> > ----> 1 max(len(rich), poor)
> > 
> > TypeError: '>' not supported between instances of 'str' and 'int'
> > ~~~
> > {: .error }
> {: .solution}
{: .challenge}

> ## Why Not?
>
> Why don't `max` and `min` return `None` when they are given no arguments?
>
> > ## Solution
> > `max` and `min` return TypeErrors in this case because the correct number of parameters
> > was not supplied. If it just returned `None`, the error would be much harder to trace as it
> > would likely be stored into a variable and used later in the program, only to likely throw
> > a runtime error.
> {: .solution}
{: .challenge}

> ## Last Character of a String
>
> If Python starts counting from zero,
> and `len` returns the number of characters in a string,
> what index expression will get the last character in the string `name`?
> (Note: we will see a simpler way to do this in a later episode.)
>
> > ## Solution
> >
> > `name[len(name) - 1]`
> {: .solution}
{: .challenge}