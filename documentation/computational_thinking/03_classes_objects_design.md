# 03 - Classes, Objects, Design

## Objects, methods, interactions

Over the last few sessions we've talked a lot about different types of **objects**, which are often stored in **variables**, and which we interact with by calling their **methods**, or by passing them as **arguments** to other methods or functions.

A quick example:

```python

drawn_cards = [
    {
        "name": "The Magician",
        "is_major": True,
        "rank": 1,
    },
    {
       "rank": 3,
       "is_major": False,
       "suit": "Swords"
    },
    {
        "name": "The Tower",
        "is_major": True,
        "rank": 16
    }
]

def draw_summary(cards):
    summary = []
    for card in cards:
        if card["is_major"]:
            summary.append(f"{card['rank']} - {card['name']}")
        else:
            summary.append(f"{card['rank']} of {card['suit']}")
    return "\n".join(summary)

print(draw_summary(drawn_cards))
```

Here we have a `list` object stored in the `drawn_cards` variable, with three entries, each of them a `dictionary` object (which have subtley different keys and values).

We also have a `draw_summary` method which takes a list of dictionaries like the one above, creates a list object in the variable `summary`, and manipulates it by calling its `append` method, appending a summary of each card in the draw, then joins them together with line breaks and returns the resulting string by calling the `join` method on a string containing the line break character.

We call it with our list of cards, and finally we call the built-in `print` method to print this summary out to the console.

We can see here examples of methods being called (`.append`, `join`) and objects being passed as arguments to functions, and we should start to get some idea of the things-that-make-an-object-an-object, at least in python terms.

An object:

 - Can be created, with some data representing its _state_ (like one of our "card" dictionaries: each one has a broadly similar "shape" (or _interface_), but the data stored inside it varies)
 - Can have methods called on it (either by appending a dot and the method name, as with `.append` on string, or with some more "special" syntax, such as the two square brackets that allow us to get a value from a dictionary: this, as we shall see presently, is also a method.)
 - Can be stored in a variable
 - Can be passed as an argument to another function or method.

(This is a kinda tentative list for now, we'll carry on refining this ontology-of-objects as we go.)


## Aesthetics, norms, and refactoring.

The example above is only one of many possible ways we could have written code to print the "draw summary" above. For instance, the following code would produce the exact same result:


```python

def card_summary(card):
    if card["is_major"]:
        return f"{card['rank']} - {card['name']}"
    else:
        return f"{card['rank']} of {card['suit']}"

def draw_summary(cards):
   return "\n".join(card_summary(card) for card in cards)

```

Note that the result of this version of `draw_summary` is _exactly_ the same as before, we haven't changed either the input it expects, or the output it returns - we have however, _extracted a method_ from the inner part of our loop. There are many other ways we could have written this method for sure (and trying to think up a few might be an interesting exercise): This process of taking a block of code and rewriting it so that it _does the same thing_ but is written differently, is called _refactoring_. Refactoring is both a normative, and an aesthetic exercise: we refactor our code to make it _better_ in some sense. But what constitutes _better_? We can think about this pragmatically: we can refactor so that our code is more _general_ (it produces a reasonable output for a greater possible range of inputs), more _flexible_ (it can be re-used in other contexts - see how, above, I extracted a separate `card_summary` method which we could use elsewhere to print out the name of a single card, which we didn't have before), or simply _clearer_ or _easier to read and understand_: I think my refactoring of `draw_summary` above achieves this: you can now clearly see that it summarises each card individually, then formats the summaries on individual lines, something that kinda got lost in the original version.

However, these values are often contested (what i find easy to read and understand might not be what you do), and are often in opposition to each other (something which is _flexible_ or _general_ may not be _clear_), so there's a situated, subjective quality to refactoring. For instance, I could have generalised this method to "summarise any arbitrary list of things, given a particular way of summarising a single thing, printing the summaries on each individual line":

```python
def summarise_list(xs, f):
    summary = ""
    accumulator = lambda summary, x: summary + f"{f(x)}\n"
    [summary := accumulator(summary, x) for x in xs]
    return summary

def draw_summary(cards):
    return summarise_list(cards, card_summary)
```

This is meant as a slightly pathological example: there's a lot of new things in here i haven't introduced you to yet ([lambda expressions](https://www.pythontutorial.net/python-basics/python-lambda-expressions/), [the `:=` syntax in list comprehensions](https://stackoverflow.com/questions/10366374/what-is-the-pythonic-equivalent-to-the-fold-function-from-functional-program?noredirect=1#comment136916819_10366374), the fact that [you can also pass functions as arguments to other functions](https://www.geeksforgeeks.org/higher-order-functions-in-python/)), and i've been deliberately, obtusely brief in my naming of arguments (using eg `xs` and `f` instead of `things_to_summarise` and `summarising_function`, for instance).

Therefore, understanding the above example is not the point, but i hope it illustates a few things about the _design_ of code, and about refactoring:

 - Firstly, that things we might find desirable in our code are often in tension. Our `summarise_list` function is more _general_ than `draw_summary` in that it can summarise any list of things, (given a way of summarising each one), but this comes at the price of readability.
 - Secondly, that ideas of what is _understandable_ or _readable_ vary wildly between individuals and between communities. The version above would probably be familiar to (and even maybe considered _elegant_ by) a fan of [_functional programming_](https://en.wikipedia.org/wiki/Functional_programming) who's used [Haskell](https://www.haskell.org/), for instance (although they would definitely balk at some aspects of it).
 - Thirdly, that there are definitely pathologically complicated, antisocial ways of achieving very simple things, and that complexity in programming is not a given, nor a good :-)

This leads me to a tentative, subjective, valuation: Working within the context of the python language, community and norms, my first refactoring was _good_, an _improvement_, while my second was extremely _bad_, even though both arguably made the code _either_ more _general_, _flexible_, or _understandable_. Therefore we might ask: what are the particularly _pythonic_ tools and techniques at our disposal when we're designing or refactoring our programs?

Python is an _object-oriented_ language, so typically "good" design takes advantage of these object-oriented properties and principles in achieving a result. And one of the most important principles of object-orientation is [_encapsulation_](https://en.wikipedia.org/wiki/Encapsulation_(computer_programming)) - the idea that all the properties of a given thing are stored together, along with methods that operate on that thing.

## Encapsulation: The class as object blueprint, initializing objects.

Let's look at the data we're operating on here, our list of cards:

```python
[
    {
        "name": "The Magician",
        "is_major": True,
        "rank": 1,
    },
    {
       "rank": 3,
       "is_major": False,
       "suit": "Swords"
    },
    {
        "name": "The Tower",
        "is_major": True,
        "rank": 16
    }
]
```

This, is already (at least partially) encapsulated - each _card_ is a discrete object. We could, for instance, have had seperate variables for `card_1_name`, `card_1_is_major`, `card_1_suit` etc. This would both be very much _not-at-all-encapsulated_, and would have severely limited the generality of our code: we'd both be limited to three card draws, and would need to know in advance which cards were major arcana and which were minor arcana, in order to know what variables we need to define (for instance, whether a card has a `name` or a `suit`).

However, there's still a couple of problems with it that we could refactor away.

The first is that modelling a card as a dictionary offers us no guarantee that it has the properties we expect (`rank`, `is_major` and  either `suit` or `name`) - nothing is stopping us adding a dictionary to that list containing information about a member of our Colla de Castellers (`{ "nom": "Xavi", "posició": "Baix", "pes": 90, "altura": 160}`), and the first time we'd find out about it is when our program crashes when we try and print the `card_summary` (what specific error would we get?).

The second, is that the _behaviour_ which is related to a single card (printing its summary) still lives elsewhere - in the `card_summary`, which breaks the principle of encapsulation.

Therefore, we can make a further improvement, by defining a new _type_ of object which specifically holds a representation of a tarot card. A _type_ of object is called a _class_, and when we define it we create a sort of _blueprint_ for other objects.

```python
class TarotCard:
    def __init__(self, is_major, rank, suit=None, name=None):
        self.is_major = is_major
        self.rank = rank
        self.suit = suit
        self.name = name

    def summary(self):
        if self.is_major:
            return f"{self.rank} - {self.name}"
        else:
            return f"{self.rank} of {self.suit}"


def draw_summary(cards):
    return "\n".join(card.summary() for card in cards)


cards = [
    TarotCard(True, 1, None, "The Magician"),
    TarotCard(False, 3, "Swords"),
    TarotCard(True, 16, None, "The Tower")
]

```

Here, we've created a new TarotCard class, which has _exactly_ and _only_ the properties we expect of a tarot card - it would be very obvious at the point where we created it, if we got confused and tried to create a tarot card using the vital statistics of Xavi the Baix instead of information about an actual card, saving us from errors and crashes later.

Also, we've given the card a summary method - it now knows how to _describe itself_ rather than relying on an external function to do that for it.

Our `draw_summary` method stays almost the same, but instead of calling `card_summary` with the each card, we call the `summary` method of the card itself.


We've introduced a few new bits of syntax here, so let's go over them one by one, starting at the end and tracing back.

```python
cards = [
    TarotCard(True, 1, None, "The Magician"),
    TarotCard(False, 3, "Swords"),
    TarotCard(True, 16, None, "The Tower")
]

```
Now, our list of cards isn't a list of general-purpose dictionaries, but a list of objects of the `TarotCard` class. These look a bit like calls to a method (except in `CamelCase` rather than `snake_case`), and they function in a broadly similar way - they take arguments, and they return something. In this case, they return an _instance_ of the `TarotCard` class which we define above:

```python
class TarotCard:
    def __init__(self, is_major, rank, suit=None, name=None):
        self.is_major = is_major
        self.rank = rank
        self.suit = suit
        self.name = name

  def summary(self):
        if self.is_major:
            return f"{self.rank} - {self.name}"
        else:
            return f"{self.rank} of {self.suit}"
```

A class definition starts with the `class` keyword, followed by the name of the class, and in the indented block, we define the class's _methods_ (using the same `def` keyword that we use to define functions elsewhere). Some of these functions have a special role (those with particular names which by convention are surrounded with `__double_underscores__`): we see one of them here: the `__init__` method, which is the class _constructor_ - this is the function which takes the arguments we pass to `TarotCard` below, and uses them to create a new `TarotCard` object.

This method has two new things we haven't seen before, one of which is particular to definitions of methods within a class, and one of which is a more general thing we can use in any function definition.

The first, which is specific to class methods, is the special `self` argumment, which is always the first argument in the list. This refers to the _instance_ of `TarotCard` which we are working with: in the constructor, we can think of this like an empty box which we can store things in: we take all the other arguments, and store them as properties on `self` so that we can get at them later.

The second thing, which we can use anywhere we define a method or a function, is the use of _optional_ arguments, or arguments which have a _default value_, shown by the equals sign after the argument name. In our case, both `suit` and `name` are optional - as major arcana won't have a `suit`, and minor arcana won't have a `name`. By providing `None` as the default argument for both, we ensure that neither of them are compulsory (we can provide _any object_ as a default, not just _None_, if there's a sensible "default value" we could provide it here).

We also provide a `summary` method which is an _almost_ exact copy of our older `summarize_card` function with a couple of key differences. First, it takes the same phantom `self` argument (when we call it, as you can see in `summarize_draw` we don't pass this argument explicitly, rather it refers to "the thing before the dot"), and we use that argument to get back the _arguments_ we provided to the constructor. which we access with the dot (to get at properties on an object), rather than the square brackets which we use to get a value from a dictionary.


Let's have a look at how we could use our new TarotCard class from the python REPL:

```
>>> card = TarotCard(True, 2, None, "The High Priestess")
>>> card.is_major
True
>>> card.rank
2
>>> card.suit
None
>>> card.name
"The High Priestess"
```

Note that all the card's _properties_ are _public_ we can access them directly from outside the class, as well as from within its own methods. This can be useful, but also a bit of a liability - sometimes we might want to keep the inner workings of our class hidden. In python, we can't enforce this, only signal it by convention - a property or method with an underscore at the beginning of its name is considered 'private' and we avoid using it outside. This is another clash of values - a programmer more familiar with Java (or some other more purist object-oriented language) would probably want some method of enforcing that these properties cannot be seen or changed from outside the class, but in Python-land we're more relaxed.

One final small improvement we can make before we move on, when we instantiate our card classes there's a little bit of mess:

```python
cards = [
    TarotCard(True, 1, None, "The Magician"),
    TarotCard(False, 3, "Swords"),
    TarotCard(True, 16, None, "The Tower")
]

```
... we have to explicitly pass "None" as the value for the suit of our Major arcana, as the name argument comes after it in the list(hence why we don't have to provide an explicit `name` of None for the minor arcana). We can do away with this by providing the `ǹame` arguments _by name_, rather than _by position_:


```python
cards = [
    TarotCard(True, 1, name="The Magician"),
    TarotCard(False, 3, "Swords"),
    TarotCard(True, 16, name="The Tower")
]

```

If we wanted to be really explicit, we could even pass every argument by name, so it's clear exactly what it is:

```python
cards = [
    TarotCard(is_major=True, rank=1, name="The Magician"),
    TarotCard(is_major=False, rank=3, "Swords"),
    TarotCard(is_major=True, rank=16, name="The Tower")
]

```

You can provide arguments to any function either by position or by name: There's a trade-off in using positional vs named arguments between explicitness and verbosity, another aesthetic concern which might lead to different value judgements in different contexts.

## Inheritance, Interfaces

This is already, I think, an improvement on what we started with, but there's one thing that still bugs me: and it's those "None" arguements for the suit and the name. The reason I don't like them, is that there's still nothing stopping us creating a nonsensical card, for instance a minor arcana without a suit or a major arcana without a name:

```python

silly_1 = TarotCard(is_major=True, rank=6, suit="Hearts")
silly_2 = TarotCard(is_major=False, rank=4, name="of coins")
```

The problem here is redundancy: we're got three bits of state which explicitly implicitly describe the difference between a major and a minor arcanum: the `is_major` variable itself, and the presence or absence of both `suit` and `name` respectively. It'd be nice to make sure there was a clear dependency between these: if an arcana is major it _must not_ have a suit, and _must_ have a name, and if it's minor, vice-versa.

To me, this is a signal that we have two types of things which are the same in some respects (and which we want to have the same `interface` -  we want to  be able to use them interchangably), but different in others (their specific internal representation and the way they're created). They're distinct _subtypes_ of a more general TarotCard type, and python (and object-oriented programming) in general offers us a way of dealing with this: _inheritance_.


Inheritence means that classes can _inherit_ behaviour and methods from a _parent_: we can use this to define _all-the-things-that-a-card-has-in-common in one place, and then deal with the specifics of major and minor arcana separately. Let's have a look at how we might do that.



```python

class TarotCard:
    # Here we would put unchanging behaviours common to all Tarot cards
    def summary(self):
        pass

    def greet(self):
        return f"I am a Tarot Card, my number is {self.rank}. I will tell your fortune!"

class MajorArcana(TarotCard):
    def __init__(self, rank, name):
        self.rank = rank
        self.name = name

    def summary(self):
        return f"{self.rank} - {self.name}"

class MinorArcana(TarotCard):
    def __init__(self, rank, suit):
        self.rank = rank
        self.suit = suit

    def summary(self):
        return f"{self.rank} of {self.suit}"


def draw_summary(cards):
   return "\n".join(card.summary() for card in cards)


cards = [
    MajorArcana(1, "The Magician"),
    MinorArcana(3, "Swords"),
    MajorArcana(16, "The Tower")
]
```

In this version, we first define "the general idea of a tarot card" in our TarotCard class - in which we signal that it should have a `summary` method, the definition of which we leave undefined for now (with the `pass` keyword). By way of illustration, I also include a very silly `greet` method here: _superclasses_ like TarotCard can have actual, real behaviour in them which is inherited by their _subclasses_, and these methods can access other methods and data (such as _rank_ which is present on every subclass).

We then define separate classes for our Major and Minor arcana, providing `TarotCard` as an argument in brackets to the class definition itself, which denotes it as the parent.

Our subclasses then need only take the data they particularly need in their constructor  - this ensures we can't have the inconsistency we noted earlier between the type of arcana and its properties - and also means that none of our arguments are optional - if we want to make a `MajorArcana` or `MinorArcana` object, we _must_ provide the data it needs.

We then define a different _implementation_ of the `summary` method for each of the subclasses, which also allows us to get rid of the `if` we needed before.

The end result is that both our Major and Minor  arcana respond to the `TarotCard` _interface_ - we can call `summary` and `greet` on either of them without caring what concrete type of card they are (this is called _polymorphism_), but each one encapsulates only the data it needs, and provides its own _implementation_ for summary. This is an example of the benefits of this type of encapsulation: nothing else that needs to deal with a tarot card needs to care about the details of its internal logic, the existence of major and minor arcana, etc, it just needs to ask it how it would summarise itself.

We've one loose end to tie up later: There's nothing stopping us creating a `TarotCard` class directly, which would be pretty useless: it doesn't provide a summary, and it would error on calling `greet` as it doesn't have a `rank`. It's an _**abstract** base class_ - it represents some shared behaviour or concept which never exists in isolation, and python provides a way of marking it as such, ensuring that we will be prevented from tying to instantiate it. We do this by making it itself inherit from the `ABC` class (for "Abstract Base Class" [in the package `abc` of the python standard library](https://docs.python.org/3/library/abc.html).

```python
from abc import ABC

class TarotCard(ABC):
    # Here we would put unchanging behaviours common to all Tarot cards
    def summary(self):
        pass

    def greet(self):
        return f"I am a Tarot Card, my number is {self.rank}. I will tell your fortune!"
```

Putting it all together, we've got the following:


```python

from abc import ABC

class TarotCard(ABC):
    # Here we would put unchanging behaviours common to all Tarot cards
    def summary(self):
        pass

    def greet(self):
        return f"I am a Tarot Card, my number is {self.rank}. I will tell your fortune!"

class MajorArcana(TarotCard):
    def __init__(self, rank, name):
        self.rank = rank
        self.name = name

    def summary(self):
        return f"{self.rank} - {self.name}"

class MinorArcana(TarotCard):
    def __init__(self, rank, suit):
        self.rank = rank
        self.suit = suit

    def summary(self):
        return f"{self.rank} of {self.suit}"


def draw_summary(cards):
    return "\n".join(card.summary() for card in cards)


cards = [
        MajorArcana(1, "The Magician"),
        MinorArcana(3, "Swords"),
        MajorArcana(16, "The Tower")
        ]

print(draw_summary(cards))
```


## Exercises

 - Try and think of another way of refactoring our first attempt at writing `summarize_draw`. What are the benefits and drawbacks of your version relative to each of the others we've derived here?
 - Go back to our version of the `summarise_draw` method where cards were represented as dictionaries. What error would we get if we accidentally included a casteller instead of a card in our draw? at what point would that error manifest itself?
 - Think of an example of a function or method which takes a default value that **isn't** none and implement it. (Clue: what if we wanted to separate the cards in our draw summary with something other than a newline?)
 - Define a class to hold a _draw_ of cards, and allow it to summarise itself.
 - Have another look at [The Zen of python](https://peps.python.org/pep-0020/) - how the are norms/values/virtutes it describes reflected (or not) in each of our refactorings?
 - `__init__` isn't the only special "double underscore" method in python - they're called "dunder methods" (why, i have no idea), and [there are many of them which do various different things](https://www.pythonmorsels.com/every-dunder-method/https://www.pythonmorsels.com/every-dunder-method/). They're typically not called directly, but are used to support other bits of python syntax. Have a look at the list at this link: which do you understand, and which not? Which might be appropriate to implement for our `TarotCard` class and subclasses? Which could be implemented in the TarotCard superclass itself, and which would need to live in the specific subclass?

_(Next Time: **Some SOLID heuristics for object oriented design**)_

_(Subsequently: **PIPs, libraries, APIs: standing on the shoulders of giants and talking to the outside world**)_

