# Working Notes 3: Roughing Out a Card Class

More to come soon.

The `card` class needs to:

- Include attributes to capture multiple techniques for reading/interpreting tarot card reversals
- Align with the (EAV, probably) data model for flexibility and extensibility
- Provide methods and a "surface" for querent interaction and personalisation
- Support querents' exploration of patterns, relationships, and narratives across the deck

What else does it need to do?

## Prototyping in-progress

```Python
class Card:
    def __init__ # (self, id, name, number ... )
    self.id = id # Card number, denoting its position within the full deck
    self.name = name # A string
    self.number = number # Card number, either within the Major Arcana, or a suit (Jodorowsky is hot on numerology)
    self.arcanum = arcanum # Major or minor (or an Oblique Strategies/MtG card, lol)
    self.suit = suit # Choice of four, which also carry elemental dignities (?)
    self.court_card # A boolean (argument being that court cards have a slightly different ontological status)
    self.keywords = keywords # Three main keywords, with room for the querent to add others at the same level, without overwriting these (though they could change their behaviour?)
    self.description = description # [?] A string of two sentences, material for NLP operations and named entity extraction?
    self.archetype = archetype
    self.named_entities = named_entities # Figure out how to name this attribute
    self.actions = actions
    self.emotions = emotions
    self.characteristics = characteristics
    self.querent_notes = querent_notes # Attached to the card as an object, but we also want to be able to append querent notes to other attributes and entities (and relations, sets, correspondences ... !)

    # Reversal attributes
    self.reversed = False # A boolean, also the trigger for the baseline "negation" reversal, which then gets overwritten by any of the following attributes
    self.obstruction = None
    self.imbalance = None
    self.shadow = None
    self.transformation = None
    self.subversion = None

    # Flip the switch
    def reverse(self):
        self.reversed = not self.reversed

    # If this is returning/transforming descriptions, need to make sure they're formatted or structured in a way that supports whatever we're trying to do with them
    def meaning(self):
        if self.reversed:
            return self._generate_reversed_meaning() # [?] Why is this prepended by an underscore?
        else:
            return self.description

    def _generate_reversed_meaning(self):
        # Placeholder for generating reversed meaning based on various attributes
        if self.obstruction:
            return f"Obstruction: {self.obstruction}"
        elif self.imbalance:
            return self.interpret_imbalance()
        elif self.shadow:
            return f"Shadow: {self.shadow}"
        elif self.transformation:
            return f"Transformation: {self.transformation}"
        elif self.subversion:
            return f"Subversion: {self.subversion}"
        else:
            return f"Negation: No {self.description}" # Too simplistic; need to work more on this

    def diagnose_imbalance(self, querent_situation): # [?] Where and how do we define the `querent_situation`?
        # Placeholder for diagnosing imbalance based on querent's situation ...
        pass

    def interpret_imbalance(self):
        if self.imbalance == "MISUSED":
            return f"Imbalance: {self.name}'s energy of {self.description} may be misused or misapplied."
        elif self.imbalance == "EXCESSIVE": # [?] ELIF?
            return f"Imbalance: An excessive or overcompensating expression of {self.name}'s {self.description}."
        # Handle other imbalance types ...
        else:
            return f"Imbalance: {self.imbalance}" # [?] Aaaaah, what does this do?

    # Got to be a better name for this function (is it a function?), surely
    def generate_subversive_prompts(self):
        prompts = [
            f"How might a trickster see the humour or opportunity in {self.subversion}?",
            f"What assumptions are being challenged by {self.subversion}?",
            f"Consider how {self.subversion} might offer a new perspective on your situation."
        ]
        return prompts

    # Less sure about all this
    def assess_relationship(self, querent_input):
        # Placeholder for assessing the querent's relationship to the upright meaning
        return "stuck" # Example output (and where does it get returned from, exactly?)

    # This is "Transformation", I think
    def propose_reversal(self, relationship):
        if relationship == "stuck":
            return "Breaking free from limitation"
        elif relationship == "resisting":
            return "Overturning resistance"
        # Add other mappings as needed
        else:
            return "Reconsidering"

    # Self-representation as a string?
    def __str__(self):
        if self.reversed:
            reversal_str = "Reversed: "
            if self.obstruction:
                reversal_str += f"Obstruction - {self.obstruction.value} - {self.obstruction_meaning}"
            elif self.imbalance:
                reversal_str += f"Imbalance - {self.imbalance.value} - {self.imbalance_meaning}"
            elif self.shadow:
                reversal_str += f"Shadow - {self.shadow.value} - {self.shadow_meaning}"
            elif self.transformation:
                reversal_str += f"Transformation - {self.transformation.value} - {self.transformation_meaning}"
            elif self.subversion:
                reversal_str += f"Subversion - {self.subversion.value} - {self.subversion_meaning}"
            else:
                reversal_str += "Negation"
            return f"{self.name} - {reversal_str}"
        else:
            return f"{self.name}: {self.meaning}"

    # Need to think about the procedural logics of appending querent-supplied values (and attributes?) to the card
    def add_querent_note(self, note):
        self.querent_notes.append(note)
```

(In this implementation, the `__str__()` string representation method checks if the card is reversed. If it is, the method checks the value of each reversal attribute in order of priority (`obstruction`, `imbalance`, `shadow`, `transformation`, `subversion`). If a reversal attribute is set, the method includes the relevant information in the string representation of the `Card` object. If none of the reversal attributes are set, the method defaults to the baseline "negation" reversal. If the `Card` object isn't reversed, the method defaults to showing the upright meaning.)

### Example

```Python
card = Card(
    id=1, name="The Fool", number=0, arcanum="Major", suit=None, court_card=False, # Guessing we can't have `id=0`
    keywords=["Beginnings", "Innocence", "Spontaneity"], description="The eternal child, filled with wonder and trust in the universe.",
    archetype="The eternal child", named_entities=["The eternal child", "The universe", "A new adventure"],
    actions=["Embarking on a new adventure"], emotions=["innocence", "wonder", "trust"], characteristics=["innocent", "spontaneous"]
)

card.reverse()
print(card.meaning())
card.add_querent_note("Querent feels uncertain about new beginnings.") # Highly relatable, tbh
print(card.querent_notes)
```

(Could be useul to think about the inclusion/implementation of a possible `shadow_archetype` attribute?)

## Desmuntar