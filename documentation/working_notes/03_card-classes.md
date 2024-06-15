# Working Notes 3: Roughing Out a Card Class

To come soon.

## Prototyping In-Progress

```Python
class Card:
    def __init__ # (self, id, name, number ... )
    self.id = id # Card number within the deck
    self.name = name # A string, I guess
    self.number = number # Card number
    self.arcanum = arcanum # Major or minor
    self.suit = suit # Choice of four
    self.court_card # A boolean
    self.keywords = keywords # Three keywords
    self.description = description # A string of two sentences, material for NLP operations and named entity extraction?
    self.archetype = archetype
    self.named_entities = named_entities # Figure out how to name this attribute
    self.actions = actions
    self.emotions = emotions
    self.characteristics = characteristics
    self.querent_notes = querent_notes # Attached to the card as a whole/entity, but also want to be able to append querent notes to other attributes and entities?

    # Reversals
    self.reversed = False # A boolean, also the baseline "negation" reversal
    self.obstruction = None
    self.imbalance = None
    self.shadow = None
    self.transformation = None
    self.subversion = None

    def reverse(self):
        self.reversed = not self.reversed

    # Need to think a bit about the procedural logics of appending querent-supplied information to the card
    def add_querent_note(self, note):
        self.querent_notes.append(note)

```

## Desmuntar