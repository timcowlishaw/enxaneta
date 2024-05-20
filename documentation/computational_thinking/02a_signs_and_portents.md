# Part 2: Signs and portents (section a)

So, in the first part we took a very deep dive into the material and historical underpinnings of computation and computational thinking, which, while not strictly necessary, was probably a valuable way of at least getting a glimpse of _how_ the arcane incantantions we write when we program in python make computers _do stuff_, and have effects out in the world, and hopefully gave you an idea of how mmuch of the programming we do is done in a way thats entangled with the work of others, rather than being ex-nihilo wizardry.

However, at root, we're composing words together which _make things happen_, which does, I guess have something in common with wizardry: programs are, in that respect, a little like spells or incantations (I found out this weekend that [the word "abracadabra" comes from the Hebrew "ebrah k'dabri,"](https://www.nationalgeographic.com/premium/article/abracadabra-meaning-malaria-spell-magic) which translates to "I create as I speak"), which is i guess an apt description of the way we work with language (in this case, programming language) in computation.

![Representation of aspects of the LISP programming language as the Kabbalistic Sepherot or Tree of life. Origin unknown but widely meme'd](https://raw.githubusercontent.com/timcowlishaw/enxaneta/main/assets/images/ct2_0_lispsephirot.jpg)

This linguistic, performative aspect of progamming - combining words in order that they _do things_ is probably more key to what it means to _think computationally_ in the way most people use the term than the material, historical stuff we discussed last time, and therefore, while I'm going to try and keep circling back to the materiality of computation throughout this series, I think this week we have to take a turn towards the abstract, the symbolic, the immaterial: what are the elements of the language that we can compose together when we write in python? Throughout this chapter (which we'll go through in a few parts), I'm going to try and provide you with a kind of partial bestiary of the types of things you encounter in a python program, and how you can interact with them.

It all sounds decidedly mystical, so, in the spirit of _commitment to the bit_ (as well as commitment to "making things that actually interest us"), we're going to do this by exploring the tarot.


First of all, I'm going to introduce you to a new trick for interacting with python, which'll help us sketch out and test things in a more immediate manner than writing code in a file, saving it, then running it, every time we want to try something. As before, switch on the raspberry pi and connect to it over SSH, and when you get to the console prompt, type in `python` (or `python3` if that gives you an error, I forget what python is called on the Raspberry pi). You should see the console prompt change to three angle brackets like this:

```
[tim@bananastand:~]$ python
Python 3.11.8 (main, Feb  6 2024, 21:21:21) [GCC 12.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>

```

This is a handy mode of the python interpreter - if you run it without specifying a file to interpret (as we did last time with our hello_world.py), it provides this interactive mode, where we can type in python expressions, press return, and have them evaluated immeditely. It's very useful for trying things out. For instance, we could add our "hello world example here":


```
Python 3.11.8 (main, Feb  6 2024, 21:21:21) [GCC 12.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> print("Hello World")
Hello World
```

It works exactly like the console we're used to, except the stuff we type in is python code. We type on the lines with the three arrows, and the output appears below when we press enter. This particular mode of interacting with Python (or with any programming language) is sometimes called a REPL, which is short for "Read-Eval-Print Loop", as thats exactly what's happening. The interpreter reads a line, evaluates it, and prints the result, then goes back to do the same thing all over again.

We talked a little the last time about _strings_ (text, identifiable by their surrounding quote marks), and _functions_: (things-that_do_ things, identifiable by their trailing parentheses), and _variables_ (words without quotes which 'store' a value of some sort, brought into existence through the equals sign), so lets take it as read that they already form part of our bestiary, although we'll discover more about each of them as we go.

The first _new_ character I want to introduce you to is the [_list_](https://docs.python.org/3/library/stdtypes.html#list), identifiable by its square brackets:

```
>>> [ "Dosos", "Acotxedor", "Enxaneta" ]
[ "Dosos", "Acotxedor", "Enxaneta" ]
```

Lists are exactly what they sound like, lists of other things (in this case, names of positions in the _pom de dalt_ of a _castell_ - each name is a _string_, as you can tell by their surrounding quotes.) Syntactically, we surround them with square brackets, and we seperate all things in the list (commonly called _elements_) by commas.

(In the example above, note also that Python parrots the list back to us after we press enter, the "print" part of the read-eval-print loop)

As with most of the types of things we're going to discuss (if not all of them: i'm being a little equivocal here as i honestly can't remember if there are any exceptions to this rule lurking somewhere), lists can be assigned to variables:


```
>>> pom_de_dalt_positions = ["Dosos", "Acotxedor", "Enxaneta" ]
>>>
```

Note that this time Python *doesn't* parrot (or _echo_ in more technical language) the list back to us. We'll go into this in more detail presently, but in general, when we assign something to a variable, we don't see it echoed back out on the screen. We can evaluate our new variable to see what's in it:


```
>>> pom_de_dalt_positions
["Dosos", "Acotxedor", "Enxaneta" ]
>>>
```

..and there are our castellers!


Lists can contain any other type of thing (including other lists!), and can contain a mixture of types of things:

```
>>> [ "Alejandro Joderowsky", 24, True, pom_de_dalt_positions ]
['Alejandro Joderowsky', 24, True, ['Dosos', 'Acotxedor', 'Enxaneta']]

```

This, slightly heterogenous list contains the name of chilean-french filmmmaker and _tarotista_ Alejandro Joderowsky, the number 24, the general idea of truth, and another list, which in turn contains the names of the three positions in the _pom de dalt_ of a _castell_.

(Note here that we referred to our variable `pom_de_dalt_positions` when we defined our slightly arbitrary list of stuff, but when the interpreter echos it back to us, it expands it out and gives us the list itself: this is an example of the _evaluation_ in the "Read-Eval-Print Loop" we discussed. No need to do much with this information for now, but note it and keep it in your mind and we'll discuss later)

One slightly sneaky thing I did here is introduce two new types of things for our bestiary in this example: the number 24 (which is an example of a type called an _integer_, or _int_ for short) and "the general idea of truth", (which is represented as the word _True_, with a capital letter, unquoted, and is an example of the type called _boolean_, or _bool_ for short).

We'll talk more about these two types when we meet them again, but as a quick introduction: booleans are the logical values `True` and `False`, written just like that, with a capital letter - we'll be thinking more about them when we come to start writing code that does things _conditionally_: "if _this_ then _that_ else _other thing_". integers are the _whole numbers_, either positive or negative. They're written just as numbers, with or without a minus sign, like: `123`, `0`, `-24`. You can do lots of things with numbers (like all the arithmetic type operations you'd probably expect), and there are other types of numbers available too, for instance, for expressing numbers that aren't whole, but we'll talk about that when we need to: one of my personal ambitions with writing this tutorial is to write an introduction to both python programming and computational thinking which contains the least amount of _maths_ as possible (or, at least, explicit, identifiable _maths_). The python documentation has a page on the [basic types](https://docs.python.org/3/library/stdtypes.html) which will tell you more about these, as well as strings, lists and everything else if you want an overview, but we'll deal more with these here in due course.

I introduce integers now though as there is one specific thing we're going to need them for, and that's one of the most basic things you might want to do with _lists_, namely "get at the things inside them". Lists are _ordered_, which means that each of their items has a defined position (or _index_) within the list (which might seem obvious, but its worth being explicit about: in the future we'll see other types of "collection of things" which dont have this property). We can use this _index_ to retrieve things from the list, using another pair of square brackets:



```
>>> pom_de_dalt_positions[0]
"Dosos"
>>> pom_de_dalt_positions[1]
"Acotxedor"
>>> pom_de_dalt_positions[2]
"Enxaneta"
>>> pom_de_dalt_positions[3]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list index out of range
```

Two important things to note here: First, the index of a list always starts from `0`, not `1`. This is a convention in pretty much every programming language, and [stems from how lists are stored in the computer's memory](https://softwareengineering.stackexchange.com/questions/110804/why-are-zero-based-arrays-the-norm) (or at least one way they can be stored). I'll get into exactly how and why this is the case when we chat, as it'll be easier with a pencil and paper, but for now, you can think of the index as an _offset_ from the start of the list: therefore the first element is element `0` because it's not offset, it *is* at the start of the list. For now, its worth noting two things: Firstly, that this, like the name of the _print_ function, we discussed last time, is another example of the material history of computation presenting itself in the abstractions we use today. Secondly, that forgetting this, and expecting `list[1]` to give us the first element of the list is entirely normal, understandable, and is perhaps one of the most common programming errors (and cause of software bugs) you'll run into: it's known as an _off by one_ error, and you will definitely run into one. Therefore if you're working with lists, and something's not working as expected, it's a very good thing to check first to identify what's going wrong.

Second important thing to note about the above: if we try and access an element of a list that doesnt exist (ie, is after the last element), we get an error! Errors also have different _types_ in this case, it's an `IndexError`, which denotes that the "list index is out of range", which is exactly the type of error we're talking about: we've tried to accesss an element of a list which doesn't exist. The stuff on the two lines above the IndexError is the _Traceback_ (also known as a _Backtrace_) of the error, this gives us information to help us locate where the error is happening in our code (but in this case its not very useful, as the error obviously happend "on the line i just typed in"). We'll get more into what a backtrace is and how to read it presently, when we're writing python code in a file instead of the REPL, as it'll be both much more useful and much easier to understand then.

(One other little detail to foreshadow stuff we'll get into later, and also to orient you with respect to terminology you will probably come across if you haven't already: When an error happens, we talk about it being "_thrown_", which always struck me as vaguelỳ Heideggerian: we suddenly encounter ourselves in a situation where an error has happened. We'll get more into what it means for an error to be _thrown_ (as opposed to say _returned_) later, as this'll give us tools for _dealing with the unexpected_ when we start writing code that does stuff like communicate with the outside world in some manner.)

Two questions / things to try out before we proceed:
 - If we committed an _off by one_ error in trying to access our `pom_de_dalt_positions`, accessing them starting from index `1` instead of `0`, how might that error manifest itself? If this isn't obvious yet, don't worry, we'll chat about it later.
 - What happens if we try to access an element of a list with a _negative_ number? Try it out, starting with `-1`.

Now we're familiar with lists, we can start building a Tarot deck.

From now on in the code blocks I may not include the three arrows denoting the point where you type, just the code to type in after them (this'll make it easier for you to copy and paste if you want. In cases where i want to draw your attention to the _result_ of evaluating a certain expression, I might still include the three arrows, but these aren't parts you'll need to copy and paste.)

Let's start with the major arcana:

```python
MAJOR_ARCANA = [
 "0 - The Fool",
 "1 - The Magician",
 "2 - The High Priestess",
 "3 - The Empress",
 "4 - The Emperer",
 "5 - The Hierophant",
 "6 - The Lovers",
 "7 - The Chariot",
 "8 - Justice",
 "9 - The Hermit",
 "10 - The Wheel of Fortune",
 "11 - Strength",
 "12 - The Hanged Man",
 "13 - ",
 "14 - Temperance",
 "15 - The Devil",
 "16 - The Tower",
 "17 - The Star",
 "18 - The Moon",
 "19 - The Sun",
 "20 - Judgment",
 "21 - The World"
]
```

Happily, the major arcana, like python lists, are numbered from zero (well, some say The Fool is _unnumbered_ but that's a semantic detail we'll gloss over for now). That means our list nicely functions as a mapping from the number of an arcana to its name:

```
>>> MAJOR_ARCANA[11]
"11 - Strength"

```

One little semantic detail to note here, I've defined our MAJOR_ARCANA variable in all capitals, which we haven't seen before. This is because its a _constant_ a thing that won't change over the lifetime of our program. naming things that are _constant_ in all caps is a _convention_ rather than a property of the syntax of the python language (nothing will preent me from changing my MAJOR_ARCANA list, but the all caps reminds me and anyone else reading the code that it's not meant to change). There's lots of examples of these sorts of conventions in programming, and particularly in Python, a language and a community which values building consensus about having a single _"pythonic"_ way of doing things. These community norms are expressed in documents called [PEP](https://peps.python.org/pep-0001/)s, or Python Enhancement Proposals, where technical details of the language, as well as community norms around its usage are debated and standardised. Of particular interest now are [PEP 20, "The Zen of Python"](https://peps.python.org/pep-0020/), and [PEP 8 - "Style guide for python code"](https://peps.python.org/pep-0008), which, in particular, includes the convention that [constants be named in all capitals](https://peps.python.org/pep-0008/#constants). there'll be lots in the style guide you don't yet understand, but it might be worth a browse for interest in any case - we can talk more about this when we chat, as i think it's one of the places where the ethnography and computational thinking sides of this project have the potential to collide in interesting ways.


Now, after that aside, let's move on to drawing a card, and we want to do so _randomly_. We could go and find some dice, throw them and then use the resulting number as an _index_ to get an element of our major arcana list, but that'd be cumbersome and time consuming, and we'd need a 22-sided dice numbered from 0, and i'm not sure such a thing exists. Much better to have the computer choose at random for us, and python can help with that, but we need to ask it:


```python
import random
```

Type the above line into the REPL - this _imports_ a _module_ called `random`, which contains a load of functions for dealing with randomness, chance and probability.

This probably merits a bit of explanation: Python includes lots of built in functionality in what's called the [_standard library_](https://docs.python.org/3/library/index.html), which, slightly tautologically, means "all the stuff that's built into python" - that link is to the documentation page which details all of it:

Obviously, we won't necessarily need everything that python gives us _for free_ in every program we write, so python gives us the opportunity to selectively reach for the things we need, when we need them, by organising the _standard library_ into _modules_, which we can include in our program using _imports_. A module is simply _a collection of related things_ (usually _functions_), and _importing_ it brings it into our program so we can use it.

Having imported `random`, its now available as a variable in our REPL:

```
>>> random
<module 'random' from '/nix/store/yvhwsfbh4bc99vfvwpaa70m4yng4pvpz-python3-3.11.8/lib/python3.11/random.py'>
```

Here, python tells us some kinda useful things about what `random` is: its a module, and its defined in a particular python file at a given location (or _path_) on your system (the particular path you get will be different to the one above, but it will end in `random.py` which is the name of an actual file on your raspberry pi, which you could open and read like any other python code). In general, any python file can be used like a module, which means we can write our own modules to organize our code, something we'll get into in a later installment of this chapter. For now thought, what interest us is what we can _do_ with this new _random_ object we've imported, and a good place to start is [its documentation](https://docs.python.org/3/library/random.html).


From the link above, one of the things that random gives us is a function called `randint` which gives us back a random integer within a range which we provide as arguments. Recall that we met the idea of a function back in chapter 1, with `print`, and that functions take _arguments_ (their inputs), might have _side effects_ (things they do) and can _return_ a value (their output). In the case of _print_, it took one argument (a _string_), had the _side-effect_ of "printing the string out to the console", and didn't _return_ anything that interested us.

`randint` is a function, like `print`, and we can describe it in similar terms: it takes _two_ arguments, both integers, one being the lowest random number we'll accept (the _lower bound_), the other being the highest random number we'll accept (the _upper bound_) and it _returns_ a random number). Unlike _print_, it doesn't have any side effects.

When we call a function within a module, we seperate the name of the module and the name of the function with a dot, and when we call a function with multiple arguments, we separate them with commas. The result of _evaluating_ a call to a function is the value it _returns_:

```
>>> random.randint(1, 6)
4
```
... the above example uses it to simulate a dice roll: i'm saying "give me a random number between 1 and 6", and it gives us a 4!


So, we could probably use this `randint` function to get a random tarot card, generating a random number corresponding to an _index_ of our major arcana list, and then using it to _get_ the card! We just need to know what the bounds of the list of arcana are: the lower bound is `0` as we discussed earlier, but we need a value for the upper bound (yes, I know its `21`, but humour me for pedagogical reasons). Whe we're dealing with a list, it's sometimes useful to know how long that list is, which we can do with the built in `len` function (for _length_).

```
>>> len(MAJOR_ARCANA)
22
```

As predicted, there are 22 cards in our major arcana.

Let's put this together with `randint` to get a random tarot card:

```python
n_arcana = len(MAJOR_ARCANA)
upper_bound = n_arcana - 1
lower_bound = 0
random_index = random.randint(lower_bound, upper_bound)
MAJOR_ARCANA[random_index]

```

Copy and paste the above into your REPL, and you should get a random tarot card!

This is all a bit verbose, but i've written it out step by step, so that you can see what's happening at each point.

First we get the number of arcana in the list, then subtract 1 to get the upper bound for our random number (if we didn't subtract 1 this would be an _off-by-one_ error: the index of the last element in the list is always one less than the length as we start counting at 0). The lower bound is pretty trivially 0, because all lists start indexing at 0, but we name this with a variable here to be explicit. We then get a random index, using the `randint` function in the `random` module we imported previously, and finally use get the element in our MAJOR_ARCANA list at that index!

We could be a bit more succinct by not bothering to store everything here in a variable with a name, this `one-liner` would give us exactly the same result (it is completely _semantically equivalent_ to the above):

```python
MAJOR_ARCANA[random.randint(0, len(MAJOR_ARCANA) - 1)]
```

This may be briefer, but even I have trouble working out what's going on here (and I wrote it, like 10 seconds ago), so I'm not convinced it's a "better" way of solving the problem. This speaks to an important aspect of programming, and of thinking computationally. There are almost always multiple ways of solving a problem, which may vary stylistically (as in the example above), trading off brevity for legibility, or might also vary _semantically_ in some sense, having subteley different behaviour, and a lot of thinking computationally is thinking through these trade-offs. In our case, neither of the two versions above I think is the "best" for our purposes, as our `random` module contains a function called `choice` which randomly chooses an element from a list for us, and it was _right there this whole time_:

```python
random.choice(MAJOR_ARCANA)

```

I'm willing to bet that if you went to find that `random.py` file where the `random` module is defined that we saw earlier, and scrolled down to where this `choice` function is defined, you'd probably see python code very like the code we wrote above, using `len` and `randint` to get the length of the list, generate a random number in the appropriate range, and then get the item in the list at that index, as that's actually a more-than-reasonable way of "getting a random thing from a list". However, its not a level of detail we want to deal with every time we want to draw a card from a tarot deck, so it makes sense to use a higher level _abstraction_ like _choice_ in this context: we don't have to repeat ourselves, going through the whole process of getting lengths and random numbers every time we want to draw a card, and it also means our intent is clearer in our code: we're _choosing a card_ rather than mucking around with indices and who knows what else, its much more readable. When we get into defining our own functions, we'll start thinking more about abstraction, and how to organise our code so that it's succinct and clearly expresses what we want it to do.

One random tarot card is cool, but really, we want to draw a spread if we want to do a reading. For now we'll draw three cards, and to do this, there's another function called `sample` in the `random` module: it will choose multiple random items from a list, _without replacement_. This means that none of the items in a given hand will be duplicates, each card is 'drawn' from the deck as in real life and the next one chosen from the remainder. there's another function called `choices`, which samples _with replacement_: this would be like shuffling the deck, drawing a card, noting it down, returning it to the deck and repeating, meaning you might see the same card twice.

To use `sample`, we pass it the list we want to draw from, and the number of items we want to draw:


```python
random.sample(MAJOR_ARCANA, 3)
```

Note that the type of the thing that `sample` returns is also a `list`, which we can see by the square brackets that surroundit.

This is all great, but if we want to get serious about tarot readings, we really want to do them with the whole deck, including the minor arcana. However, there's 54 of them, and writing them out individually, would be time-consuming, and, quite frankly boring, and, [as is supposedly fitting of programmers, we are lazy](http://wiki.c2.com/?LazinessImpatienceHubris). Furthermore, constructing a list of all the minor arcana is exactly the sort of task that computers excel at doing, as there's some useful hidden structure in there. Instead of just considering all 54 cards as individuals, we can notice that they're composed of four suits, each of which have cards of the same fourteen ranks. We can take advantage of this repetition, and get python to do the work of enumerating each individual card.

Let's start by defining the suits, and the ranks of the minor arcana. Like the major arcana, we'll define them as _constants_ (in all caps) as they're things that won't change:

```python

SUITS=["Wands", "Swords", "Cups", "Pentacles"]
RANKS=["Ace", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Page", "Knight", "Queen", "King"]

```

We might debate the order of these (Joderowsky definitely would), but it doesn't matter too much as we're going to shuffle them before we draw them. What matters is that we now have two lists, one each of the suits, and the ranks, and we can use them to create a list of all the minor arcana:

```python
MINOR_ARCANA = [f"{rank} of {suit}" for rank in RANKS for suit in SUITS]

```

... which we can do in a single line! Its a line that introduces two new concepts we haven't seen before though, so i'll explain them before we go any further:

The first _new thing_ is whats called an "[f-string](https://docs.python.org/3/tutorial/inputoutput.html#formatted-string-literals)" (short for _formatted string literal_), and it looks exactly like the strings we already know, except it has an "f" before the opening quote. F-strings are special, and useful, as they provide an extra bit of syntax within the string itself, the curly braces which allow us to substitute in (or _interpolate_) a variable we've defined outside the string:

```
>>> name = "Justin"
>>> print(f"Hello, {name}!")
"Hello, Justin!"

```

And its easy to see how this is useful for composing strings that follow a pattern, like the names of the minor arcana:

```
>>> rank = "Knight"
>>> suit = "Swords"
>>> f"{rank} of {suit}"
"Knight of Swords"

```

However, where are the `rank` and `suit` variables coming from in our example above? From our `RANKS` and `SUITS` lists via a fantastically useful bit of syntax called a [_list comprehension_](https://docs.python.org/2/tutorial/datastructures.html#list-comprehensions).

List comprehensions, from the outside, look like lists (they're surrounded by square brackets), but inside the square brackets, you'll see the keywords _for_ and _in_. They allow us to _iterate_ over a list, doing something to every element in turn, and giving back a list of the results. For instance, if we wanted to add ten to a list of numbers (sorry, i didn't want to do maths examples, but allow me one, just to keep things simple):

```
>>> numbers = [1, 2, 3, 4]
>>> [n+10 for n in numbers]
[11, 12, 13, 14]
```

You can think of a list comprehension as a thing that has three sections. First is "the thing we're gonna do to each element of the list", with "the thing in the list" represented by a variable, in this case "n". Then, after the keyword "for" we write the name of that variable, to identify how we're referring to "each thing in the list", then after the keyword "in" we put the list we want to operate on.

Another example, lets say we wanted to encourage each member of our pom de dalt, as they make their way up the castell:

```
>>> [f"Som-hi {position}, cap amunt!" for position in pom_de_dalt_positions]
['Som-hi Dosos, cap amunt!', 'Som-hi Acotxedor, cap amunt!', 'Som-hi Enxaneta, cap amunt!']
```

Here we combine the f-string we learnt just now with the list comprehension, to create a message of encouragment ("Let's go, {position}, upwards!") for each of the positions.

One other particularly handy thing about list comprehensions is that we can iterate over two lists _at the same time_, doing something with every combination of things in the two lists:

```
>>> [x*y for x in [1,2,3] for y in [2,4,6]]
[2, 4, 6, 4, 8, 12, 6, 12, 18]
```
(another slightly arbitrary mathematical example, but i think it shows the syntax clearly: we multiply every pair of numbers from two lists of numbers).

You might hear this notion of "every possible pair of things in two lists" called, in super technical/math-y terms, the [_cartesian product_](https://en.wikipedia.org/wiki/Cartesian_product) of those two lists.

So, putting together all the above, using a _list comprehension_, we can take _the cartesian product_ of the suits and ranks, then use an _f-string_ to _format_ the name of each individual card, and we get to the definition we started with, which i'll repeat here:


```python
MINOR_ARCANA = [f"{rank} of {suit}" for rank in RANKS for suit in SUITS]

```

Now we've got lists of our major and minor arcana, and creating a full tarot deck is just a matter of appending them to each other (_concatenating them_), which we do by addition ('adding' a list to another just means joining them together - this theme of "doing mathsy things with things that arent numbers" will repeat itself as we get more into what it means to "think computationally"):

```python
TAROT = MINOR_ARCANA + MAJOR_ARCANA

```

... and now we've got our complete tarot deck, it's a simple matter to draw a three card spread from it, as we saw before:


```python
random.sample(TAROT, k=3)

```

This gives us back an array of three cards, but what if we wanted to `print` out each card clearly on its own line? We can [_iterate_](https://docs.python.org/3/tutorial/controlflow.html#for-statements) over the array of cards that `sample` returns to us, using an bit of syntax that's a very close cousin of our list comprehension:


```python
for card in random.sample(TAROT, k=3):
    print(card)

```

This, just like in the list comprehension, is iterating over the list of three cards that is returned from our call to `random.sample`, assigning each one in turn to the variable `card`, then repeating the indented `block` of code underneath for each one. Unlike in the case of the list comprehension, nothing is returned from this: in the block we're calling `print` for its _side-effect_ of printing the name of the card to the screen. We use this syntax (as oppoosed to the list comprehension syntax) when we want to do something to every element of a list, but we're not bothered about the resulting value of it, like printing.

You can copy and paste the above block into the REPL, and hit enter and it should ´just work´, but i'm also going to show you how it looks on screen as there's a slightly subtle syntactic thing here which you won't have seen before that i need to point out:

```
>>> for card in random.sample(TAROT, k=3):
...     print(card)
...
15 - The Devil
Nine of Cups
Nine of Pentacles
```

Note how, after you type the first line, which ends in a colon, when we press enter, the prompt changes from three arrows to three dots. This denotes that what you're typing is going to be part of the indented _block_ of code which we repeat for each card. We still need to actually indent it though, so if you're typing this out by hand, put four spaces before the word "print". When weŕe finished defining our indented block, we press return an extra time and the whole thing is evaluated (see the extra blank line with three dots, this is where i pressed enter a second time). After that, we see the three cards printed out.

Why do we have to indent, and why do we use four spaces?

The answer to the first question is the thing i personally find most irritating about python: it's a language that has what's called _significant whitespace_, which means that indentation and spacing _actually has semantic meaning_, a thing that not all languages have (but which you'll already be familiar with from markdown: think about nested bulleted lists, for example). The whitespace denotes the semantic nesting of code: the indented block is "inside" the for-statement, its the thing that is repeated for every card in the spread.

This makes intuitive sense, so why does it annoy me so much? The answer has a little to do with why we use four spaces above. The python interpreter doesn't care if you use four spaces, or one, or two, or thirteen, or a single _tab_, or twelve tabs, or three spaces and five tabs, or whatever, as long as the "inner" bit of the loop is indented more than the outer bit. However, the interpreter _does_ care that every line is indented consistently, that you use the same amount and type of space on each line, and this leads to some deeply annoying problems if we don't take care: if, for instance, on one line we use four spaces, and on the next, a tab, both lines will look _identical_ to us, but the interpreter will refuse to run it, and it'll be difficult to identify exactly where the problem is, as it's caused by _blank space_. The solution to this in the python communuty (which is set out in the style guide PEP we linked to above) is to always use four spaces for indentation: a social solution to a technical problem.

This seems like a funny place to stop (on the vaguaries of python syntax rather than anything more profoundly computational), but we've covered more ground than i was expecting and I think this gives us a fair bit to discuss next time we meet! In the next section, we're going to think about developing a slightly richer model of the tarot deck, and in doing so, think about defining our own types-of-things to use in python programs, our own functions to do things with them, and also start interacting with the outside world in different ways.

For now, to leave the python REPL, and get back to your regular terminal, press ctrl and D, and I'll leave you with a few things to do and to ponder before we next meet.

### Things to do / think about:

- Try and take Take what we've done above, and convert it into a python program (ie a file called something like `tarot.py`), which when we run it with `python tarot.py` prints out the names three random arcana from the tarot.
- Read "The Zen of Python". Which of these lemmas do you feel you understand and which not? is there terminology here that needs explanation? What do we think might be the values or community norms which gave rise to these lemmas? What do we think of them?
- The REPL, which we've been interacting with above, takes a single _expression_ on each line we type, and _evaluates_ it when we press enter. Having played with it a bit, have a think about how you might describe or define (however provisionally) what an _expression_ is, and what _evaluation_ does. We'll talk more about this when we next chat!


