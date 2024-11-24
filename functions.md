# Functions

**Functions** are blocks of code that we can reuse in our programs. They help us not repeat ourselves when writing code. Here are other reasons you may want to use them:

### DRY

There's this concept in programming of **Don't Repeat Yourself (DRY)**. Once you start copying and pasting a bunch of code, that's a sign that you should probably put in a function.

This will help you write succinct and clean code.

### Abstraction

Abstraction is the art of simplifying our code so we deal with less and less problems. Separating your code to multiple functions allows you to test your code easily and debug faster. It also helps others (and you) have a better understanding of what your code is doing.

---

## Functions and arguments

Functions in python are created using the `def` (define) keyword, followed by the name of the function and then parenthesis and a colon. Inside parenthesis you put all arguments you will use in the function. Next you include the body of the function indented four spaces (four spaces by convention). Here's an example of a function.

```python
def greet(name):
    print('Hello, ' + name)
```

The above function takes in a name of the user as an argument and greets them. 

Functions don't always have to have arguments. Sometimes functions take no arguments at all, just like the `greet_the_world` function below.

```python
def greet_the_world():
    print('Hello, world!')
```

Functions can also have optional arguments. With optional arguments you have to provide default values. Below is an example of a function that takes in an optional argument `name`. If `name` is not provided, name will be set to the default `world`.

```python
def greet(name='world'):
    print('Hello, ' + name)
```

---

### Advanced Function Arguments (Optional)

Sometimes you need to create functions without determined arguments. The same function can take zero, five, ten, or even more arguments. This can be useful in a lot of different scenarios. Look at the function below:

```python
def sum(*arguments):
    total = 0
    for arg in arguments:
        total += arg
    return total
```

The above functions have flexible arguments. It allows the user to provide as many or little arguments and sum will handle all cases.

Here are examples of how `sum` can be used:

```python
sum(1) # 1
sum(1, 1) # 2
sum() # 0
sum(5, 2, 6, 2) # 15
```

The **asterick (\*)** is known as the ***unpacking operator***  is used to unpack lists, tuples, and generators. 

In our above example `arguments` will be a tuple and we can iterate over it.

We can also spread keyword arguments. Again, you don't normally unpack arguments in functions, but it's useful to know in case you need flexible arguments.

```python
def greet(name, **kwargs):
    print(f'Hello, {name}')

    for key, value in kwargs.items():
        print(f'{key}: {value}')

greet('Jon', city='Pretoria', age=25, hobby='Coding')

# Will print:
# Hello, Jon
# city: Pretoria
# age: 25
# hobby: Coding
```

The above function takes one required argument `name` and accepts extra keyword arguments. The **double astericks (\*\*)** are used to unpack a dictionary.

---

## The return statement

We usually write functions to perform one task and then return a value. They usually take in inputs, run some processes, and return some output.

Below is a function that adds two values together and return the results.

```python
def add(a, b):
    c = a + b
    return c
```

The `return` statement in a function is used to send a value (or multiple values) back to the place where the function was called. It essentially exits the function and provides the result of the function's execution to the caller.

Sometime we forget to return the results of the function. Usually that results in an error that may look like this `TypeError: unsupported operand type(s) for *: 'NoneType' and 'int'`.

One thing to note, the `return` statements ends the execution of a function. This means everything after the `return` statement won't be executed. Here's an example:

```python
def greet():
    print('Hello')
    return 
    print('This will not run')

greet()

# This will only print:
# Hello
```

The function only printed 'Hello', and the second `print` statement wasn't executed.

Functions can return other functions or complex objects like lists, dictionaries, or instances of classes. Below is an example of a function that returns another function.

```python
def create_greeter(greeting):
    def greet(name):
        print(f'{greeting}, {name}!')
    return greet
```

The above function is interesting because it can create different `greet` functions that greet people in different languages. Here's an example of how it could be used to greet people both in English and French.

```python
# Create an english greeter
greet_in_english = create_greeter('Hello')

# Create a french greeter
greet_in_french = create_greeter('Bonjour')

# Greet Sarah in english
greet_in_english('Sarah') # will print 'Hello, Sarah!'

# Greet Sarah in french
greet_in_french('Sarah') # will print 'Bonjour, Sarah!'
```

The `return` statement is important for many reasons. Among them is that it enables us to create a better structure of programs by breaking complex logic into smaller, testable, and reusable functions.

---

## Recursive Functions

Recursion is a technique by which a function makes one or more calls to itself during execution. They are often used to solve problems that can be broken down into smaller bits. 

They often have a recursive case and a base case to ensure that the operation stops at some point. 

To demonstrate the mechanics of recursion, we begin with a simple mathematical example of computing the value of the ***factorial function***.

```python
# factorial(5) = 5 * 4 * 3 * 2 * 1

# factorial(4) = 4 * 3 * 2 * 1

# factorial(3) = 3 * 2 * 1

# factorial(2) = 2 * 1

# factorial(1) = 1
```

By looking at the factorial of the above numbers, you can deduce that the factorial of 2 is `2 * factorial(1)`, the factorial of 3 is `3 * factorial(2)`, the factorial of 4 is `4 * factorial(3)` and so on. In fact we can conclude that the factorial of n is `n * factorial(n - 1)`.

There's a natural recursive definition for the factorial function. Here's the implementation:

```python
def factorial(n):
    # Base Case
    if n in [0, 1]: return 1

    # Factorial Case
    return n * factorial(n - 1)
```

Note that without the base case this function will run forever. So, always remember to add a base case to your recursive functions (a point that terminates the execution).

---

## Lambda Functions

The `lambda` keywords allows us to create one-line functions. They are often used for short, simple operations where defining a full function might be unnecessary.

Format:
```python
variable = lambda arguments: function body
```

Lambda functions don't need the `return` statement as the function body is evaluated and the results are returned by default.

If the function body doesn't need any arguments, you can omit them. 

Example of the `greet` function that takes in `name` as an argument:

```python
greet = lambda name: 'Hello, ' + name
```

Example of the `greet` function that doesn't take in any arguments:

```python
greet = lambda : 'Hello, world'
```


## Good to Know (Optional)

### Naming conventions

1. Functions names should be in **snake case**. They should be in lowercase and spaces should be replaced with underscores.

2. Function names should be verbs. This is because functions are supposed to do stuff. Verb-based names make the purpose of the function obvious to readers.

```python
# Bad
def addition(a, b):
    pass

# Good
def add(a, b):
    pass

# Bad 
def validation():
    pass

# Good
def validate():
    pass
```

3. ***Single Responsibility Principle (SRP)***. Functions should exist only for one purpose. This keeps your code clean, readable, and robust.










