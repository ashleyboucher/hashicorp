## Exploring Tuple Syntax
Now that you know a little bit more about the difference between a tuple and a list, let's take a look at some code:

Here we have a python list:

```python
# A list
groceries = ['apples', 'oranges', 'lettuce', 'cheddar cheese']
```

To convert this list to a tuple, we can do one of two things: remove the square brackets entirely, or replace them with parentheses.

```python
# A tuple!
groceries = 'apples', 'oranges', 'lettuce', 'cheddar cheese'

# Also a tuple!
groceries = ('apples', 'oranges', 'lettuce', 'cheddar cheese')
```

Both syntaxes are valid: it's the comma that makes something a tuple, not the parentheses. The parens, however, add helpful visibility and readability to your code.

Unlike lists, the requirement of separating each item by a comma also applies to tuples with only one item, whether or not you add the parentheses.

If a tuple only has one element, that element must be followed by a comma, otherwise the python interpreter will assume that you're _referencing_ the item in question, and not creating a tuple.

Code like the following will not produce a one-item tuple. If this code were run in a python interpreter, it would assume that I'm intending to assign the integer 1 to the my_tuple variable.

```python
# Not a tuple
my_tuple = 1
```

This is also the case if I use parens.

```python
# Also not a tuple
my_tuple = (1)
```

The comma is what makes a tuple:

```python
# A tuple!
my_tuple = 1,

# The same tuple!
my_tuple = (1,)
```

## Tuple Ordering and Indexing
Just like lists, tuples are ordered. _Ordered_ means that each element in a tuple will always fall in the same location within the tuple. This is handy: Having an ordered sequence means we can loop through it predictably. This is because all Python sequences, including tuples, are numerically indexed, beginning with 0, meaning each element in the sequence has a number indicating its position in the sequence.

This also means that individual items in a tuple (or any sequence) are accessed the same way as items in a list. 

Take the following tuple:

```python
game_of_thrones_characters = ('Sansa', 'Brienne', 'Tyrion', 'Jon', 'Cersei')
```

To access the third item in this tuple, 'Tyrion', I would use the syntax:

```python
game_of_thrones_characters[2]
```

Likewise, to access the first item, 'Sansa', I would use the syntax:

```python
game_of_thrones_characters[0]
```

All of the same operations that work on lists will also work on tuples, with the exception of mutable operations - or ones that change the list, because as we know, tuples are immutable!