# Part 2: Signs and portents (section b)

Continuing with our bestiary of python objects, there's three more creatures we will encounter along the way, the _dictionary_ and the _tuple_, and the object _None_, which i'd like to introduce you to, Next time we will start thinking a little about how we might combine these types of things, and start thinking up new creatures of our own to inhabit our python programs.

Head back into the python REPL as we did before so you can follow along with the examples.

We'll start with the _tuple_. In the first part of this section we met the _list_, contained in square brackets, and containing an arbitrary length of _other things_:

```python
a_list = [1, 2, 3, 4]

```

A tuple, at first glance, looks more or less the same, but with normal round brackets:

```python
a_tuple = (1, 2, 3, 4)
```

They're both collections of things, enclosed in brackets, and one might be forgiven for thinking that they're a bit redundant, unless  we're got specific aesthetic commitments to the brutalism of the square bracket, or the more delicate curve of the parenthesis. However, there's a few differences between the two that are worth highlighting: some which are technical in nature (in the sense that they behave in different ways), and some of which are more conventional or stylistic (in the sense that people generally use them in different ways).

The first, technical difference, is that lists are _mutable_ while tuples are _immutable_: This means, that, while we can _change_ lists any time we like, after a tuple is created, it always contains the same things. Let me introduce you to a few more things we can do with lists, which, modify them:


```
>>> castell = ["Piña", "Folre", "Manilles", "Tronc" ]

```
First things first, I used the castillan word "Piña" above, instead of the catalan "Pinya", which is enough to get me kicked out of the Colla. We can correct that by replacing it, _assigning_ a new value in position 0, using the equals sign. There's an obvious symmetr here with how we access list elements by their index, using square brackets, except this time we're putting something in rather than taking it out.


```
>>> castell[0] = "Pinya"
```

Note that nothing gets returned to us here, we just get a new `>>>` prompt. But we can check and see that the list indeed been updated:

```
>>> castell
['Pinya', 'Folre', 'Manilles', 'Tronc']
```

Another thing we can do is add a list to another one:

```
>>> pom_dalt = ["Dosos", "Aixecador"]
>>> castell += pom_dalt
>>> castell
['Pinya', 'Folre', 'Manilles', 'Tronc', 'Dosos', 'Aixecador']

```

Here we used the `+=` operator which we haven't seen before, which is called "add in place" - it adds its two arguments together, and _replaces_ the first one with the result.

We can do this anywhere we might want to add two things, not just lists:

```
>>> number = 10
>>> number += 10
>>> number
20
>>> greeting = "Hello "
>>> greeting += "Justin!"
>>> greeting
"Hello Justin!"
```

Finally we can `append` a single element to a list:

```
>>> castell.append("Enxaneta")
>>> castell
['Pinya', 'Folre', 'Manilles', 'Tronc', 'Dosos', 'Aixecador', 'Enxaneta']
```

This is all useful stuff, but I mention it in particular because these are mostly things we _can't_ do with tuples, as they involve _mutating_ the list (changing it, after the fact).

```
>>> castell_tuple = ('Piña', 'Folre', 'Manilles')
>>> castell_tuple[0] = 'Pinya'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
>>> castell_tuple.append("Tronc")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'tuple' object has no attribute 'append'

```

So we can't update an element of a tuple in place, or `append` to it, in each case it throws an error, as we saw last time when we tried to get an element of a list that didn't exist (Note that we're seeing different types of errors cropping up too: To the `IndexError` that we met last time, we can add `TypeError` and `AttributeError`. For now, simply take note that errors can have different types, and we'll talk more about what we can do with them in future).

There are, however, a couple of things we can do with tuples which might surprise us, given that they're supposedly immutable. We can use `+=` to append to them:

```
>>> castell_tuple += ('Tronc', 'Dosos', 'Aixecador', 'Enxaneta')
>>> castell_tuple
('Piña', 'Folre', 'Manilles', 'Tronc', 'Dosos', 'Aixecador', 'Enxaneta´)
```

This is for a slightly subtle reason (and i'm probably digressing a bit now, but i think its interesting, and instructive): the `+=` works differently to `append` internally. `append` take the existing list, and adds to the end of it, whereas `+=` replaces the entire list (or tuple) with a new copy, including the additional elements. In this way, even though it looks like we're mutating our castell_tuple, in fact we're not - the tuple itself never changes, but the _reference_ that the `castell_tuple` variable represents, gets updated to point to the new one. This is an important thing to bear in mind, that while certain python object (or _data structures_) might be _immutable_, variables themselves (which are _references_ to those objects) are always themselves mutable. This can also have some weird effects: consider a tuple that contains a list:

```
>>> things = []
>>> tup = ("These are a few of my favourite things", things)
>>> things.append("Castells")
>>> things.append("Ethnography")
>>> things.append("Python")
>>> tup
('These are a few of my favourite things', ['Castells', 'Ethnography', 'Python'])
```

In this example, `tup` is a tuple, which is immutable, but it contains `things`, a list which ìs mutable. Immutable objects can hold references to mutable ones, and this doesn't make the "inner" object immutable. This stuff can get confusing fast, and is often a source of bugs or other unexpected behaviours. In general, a good way of avoiding this is to keep mutation to a minimum (although in python at least it's pretty hard to avoid altogether) - we'll talk more about ways of doing this.


So having talked about a "technical" difference between lists and tuples, I'd like to talk a bit about a difference in how they're used, which kinda follows on from this techincal property. Lists, due to their mutability, are often used for accumulating things over time. Imagine we have a text file on disk containing a text (at the path "/home/justin/documents/important_text.txt"), and we want to read it in python line by line, in order to do something with it later.

```python
file = open("/home/justin/documents/important_text.txt")
lines = []
for line in file.readlines():
    lines.append(line)
file.close()
```

Here we use the built in `open` function to [open](https://docs.python.org/3/library/functions.html#open) a [file](https://docs.python.org/3/glossary.html#term-file-object) on disk, we create an empty array to hold the lines of our text, then we iterate over the lines of that file, and store them away into our array, (before _closing_ the file again - it's important to be a good citizen of the computer when dealing with shared resources like files: if we hang onto references for things like files longer than we need them, it can cause problems for us and for other programs that might need to access them).

(As well as introducing a few new things incidentally, this is a slightly torturous example: in reality there's a far simpler and more idiomatic way of opening a file, doing something with it, and closing it than explicitly closing it like this - but i'm not _quite_ ready to introduce you to some of the syntax, so consider this a slight foreshadowing of something to come. The other thing is that the iteration here is kinda redundant - `file.readlines()` returns a list, so we could just assign that list to our `lines` variable, and we're done. However, this idiom of "make an empty array then use a loop to populate it by appending new items" is one you'll definitely encounter in other contexts!)

Once we have our list of lines, we then typically want to do something with them. Lets imagine we have a function called `oulipo_n_plus_seven` which takes a string and manipulates it according to the [oulipo n+7 algorithm](http://www.spoonbill.org/n+7/) (we don't have this function, but it would be a VERY good exercise to try and write it!) - we could then use a list comprehension:

```python

oulipoed = [oulipo_n_plus_seven(line) for line in lines ]
```

Then we could for instance print out the newly oulipo-ed lines of our text:

```python

for line in oulipoed:
    print(line)

```

This example illustrates a couple of things that are common to the way in which we use lists. Typically we don't know, when we write our program, how long they are going to be (our file might have no lines, or one, or a million) - so we use them in cases where we have collections of length that might vary. The other property that follows from this is that lists are typically _homogenous_ - all the elements of them are the same type (even though this isn't actually enforced by the language, as we saw last time) - the lines of a file are all strings. Taken together, these two properties are what make _iteration_ a common pattern for interacting with lists: we do the same thing to every element (which we can do when the list is homogenous), and the fact that iteration doesn't care about the length of the list (it just goes on til its done) means that it can cope with lists of arbitrary length.

Tuples, by contrast, we tend to use for when we've got some _structure_ of two or more different things we want to keep together. Thiscould be as simple as a two-dimensional co-ordinate:

```python
point = (-1.01, 5.03)
```

...or it could be as complicated as a Casteller's vital statistics:
```python
# (Name, age, position, weight, height, passed_safety_course)
casteller = ("Xavi", 45, "Baix", 90, 150, True)

```

Tuples we typically wouldn't iterate over - it's likely they'd be heterogenous, which means it likely wouldn't be appropriate to apply the same function to every item (you're probably not gonna want to do the same thing to a name, an age, a weight in the record above, for instance). In addition, we probably have some idea of their length and format in advance (two floats for a cartesian coordinate, a set of individual attributes for a casteller record). One thing we might do when we encounter them is _destructure_ them:

```python
(name, age, position, weight, height, safety_passed) = casteller
print(f"{name} ({age}) és un {position}, fa {height}cm i pesa {weight}kg")
#=> Xavi (45) és un Baix, fa 150cm i pesa 90kg
```

... this way we can keep things we care about (all Xavi's personal details) together, but get at them all indivudually when we need to.


This is handy of course, but it also comes with a slight issue: our casteller record contains two strings, three integers, and one boolean, but it doesn't tell us what each of them means. We have to remember the order we used in its definition, and use it consistently everywhere, or we might end up accidentally treating an age as if its a weight, or a name as if it were a position - neither of which are ideal if you're trying to build a castell. It would be much better if we could label each attribute of Xavi's record so that we kknow what it is, and that is exactly what a dictionary is for!


```python
casteller = {
    "name": "Xavi",
    "age": 45,
    "position": "Baix",
    "weight": 90,
    "height": 150,
    "passed_safety_course": True
}

```

A dictionary is made up of _keys_ and _values_, and _maps_ from one to the other. So we can now ask for each individual attribute of our casteller by its key, the same way as we can take a value from a list or tuple by its position:

```python
casteller["name"]
#=> "Xavi"
casteller["weight"]
#=> 90
```

One limitation of dictionaries that we have to be aware of is that there's no guarantee that they _have_ a particular key, and if we try and get the value of a key that doesn't exist, we get an error, just as if we try and get an element from a list that doesn't exist:

```
>>> casteller["nunber_of_performances"]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'number_of_performances'

```

One way to deal with this is to use the `get` method on the dictionary, instead of the square brackets, which fails in a slightly more gentle way. Instead of throwing an error, it returns the special value `None`, which signifies the absence-of-a-thing:

```python
if casteller.get("number_of_performances") == None:
    print(f"{casteller["name"]} no ha participat en cap actuació")
    casteller["numer_of_performances"] = 0
```

We can see in the above example how we can test for the presence or absence of a value to start dealing with things-that-are-optional, and that we can also _mutate_ dictionaries, the same as we can with lists.

We've now met most of the main-character types-of-object we'll encounter in python, which should give us the tools to start sketching out the entities that populate our own programmes, but there are many many more, both in the standard library and that we'll meet elsewhere, as well as ones that weĺl define ourselves - so understanding how they are defined is going to be crucial: both to read and understand existing  definitions as well as to write our own. Therefore in the next chapter we'll begin to talk about Classes in general: a class being a "blueprint" for a particular type of object, and the key tool in doing object-oriented programming.
