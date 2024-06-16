# Working Notes 4: Roughing Out a Spread Class

## "Yes, but what _is_ a spread?"

A _spread_, in tarot, is the specific layout or arrangement of cards used for a reading. It provides the structure and positions into which the cards are dealt. Each position in the spread has a predefined meaning or interpretation that contextualises the card placed there. (link with anthropologist Pascal Boyer on "ostensive detachment")

An externally supplied context, or scaffold for eliciting/isolating salient details of the situation or predicament? Like a thrown quadrat? A way of cutting through the noise? Forcing the querent/reader to do reparative work, working to bridge/align the pre-defined meanings of the cards and the pre-defined meanings of the positions. A question of combinatorics?

### [?] Oh god what's the difference between a "spread" and a "reading"?

A _reading_, then, is the actual act of interpreting the cards dealt into a spread. It involves considering the meanings of the individual cards, their positions in the spread, and the relationships and patterns formed between them. A reading is the dynamic, emergent process of deriving insights from the static structure of the spread. 

| Spread     | Reading                      |
| :--------- | :--------------------------- |
| Structure  | Meaning                      |
| Predefined | Emergent                     |
| Layout     | Interpretation               |
| Potential  | Actualisation                |
| Class?     | Object? (or another Class?)  |

A reading would need to include `querent`, `question`, `date`, `reading_summary`, etc.

## Prototoyping in-progress

The class design should consider the philosophical perspectives of embodying worldviews through structure (Bogost's procedural rhetoric) and facilitating fluid, emergent interpretations (Jodorowsky's approach).

The class should align with the chosen data model (likely an Entity-Attribute-Value or EAV model) to ensure flexibility and extensibility in representing card attributes and meanings. The class should also provide a "surface" or interface for the querent to interact with, aligning with our goals of enabling self-discovery and personal growth.

Need to think again about the difference between the `Spread` class and individual `Spread` object instances.

I think we're using a JSON-style format for card data, which the `Spread` class will need to interface with to access card meanings and interpretations.

The interactions a querent has with the `Spread` class (selecting a spread, dealing cards, exploring interpretations) can enact/encode the tarot's worldview and enroll the querent in the process of meaning-making.

The `Spread` class could (eventually) provide ways for querents to manipulate the spread structure directly (or directly-ish), rearranging cards, defining custom positions, or creating entirely new spreads. Graphical or interactive representations of the spread would help querents grasp the complex relationships and emergent meanings, making the abstract concepts of tarot more tangible. This "hands-on" engagement allows querents to "think through" the tarot system.

The `Spread` class could support the evolution of spreads over time, allowing querents to save, modify, and build upon their spreads and interpretations. This supports the idea of the tarot as a "living mirror" that grows with the querent. Capturing querent reflections, insights, and personal symbolism within the `Spread` class data could create a dynamic, ever-expanding cathedral of meaning.

(Note: The final version of the program will not handle randomisation or card drawing directly, requiring the use of a physical tarot deck by the querent.)

### Questions

- [?] Will the `Spread` class be responsible for generating or drawing cards from the deck, or will it only handle the arrangement and interpretation of a pre-drawn set of cards?
- [?] Should the `Spread` class handle the logic for different types of spreads (e.g., Celtic Cross, Past-Present-Future, etc.), or will there be separate classes for each spread type?
- [?] Is the `Spread` class expected to provide interpretations based on the positions and relationships between cards, or will it primarily focus on arranging the cards according to the spread layout?
- [?] Are there any specific requirements or constraints regarding the data structure or representation of the spread (e.g., using a list, dictionary, or custom data type)?
- [?] Should the `Spread` class handle any user input or interaction, such as prompting the user for a question or allowing them to choose a spread type?
- [?] Should the `Spread` class incorporate any attributes or methods to support the "Bogostian-Jodorowskian" approach mentioned in the data model notes, such as procedural rhetoric, philosophical carpentry, or approaching the tarot as a "living mirror" or "nomadic cathedral"?

### Core functionalities

- **Define meanings for each position spread positions**: Primary functionality; the `Spread` class should have a way to define the number of card positions in a spread, and store their corresponding meanings or interpretations.

- **Storing and managing the cards in the spread**: The `Spread` class should maintain a data structure (e.g., a list or dictionary) to hold the cards dealt into each position of the spread.

- **Facilitating the dealing of cards into the spread**: The `Spread` class may need methods to interact with a `Deck` class to populate itself with cards (like a digital twin??), either randomly (initially) or based on user input (later). We may need to implement a card-drawing logic within the `Spread` class itself?

- **Enabling the interpretation of the spread**: The `Spread` class should provide methods to access the cards and their positions, allowing the program to generate interpretations based on the specific layout and card combinations.

- **Display spread**: The class should have functionality to display/visualise the spread, showing the cards in their respective positions, along with their interpretations based on the spread position meanings. (Will need to think about user interface and GUI, eventually, and/or how this interacts with a physical spread in the material world.)

- **Handle reversals**: The class should account for the possibility of reversed card positions (currently handled by the `Card` class), and provide mechanisms to interpret their meanings accordingly.

- **Support multiple spreads**: The program will need to support different types of spreads (e.g., three-card spread, Celtic Cross spread), so the `Spread` class should be flexible enough to accommodate various spread configurations. (I guess we need to look at extreme cases, outliers, etc.)

### Roughing out the class

(_This_ is the point where I'm starting to struggle with the difference between a class and an object, it turns out. Like, is the `Spread` class storing the procedural rules for a particular type of spread layout, or is it providing a blueprint to be populated, anticipating its instantiation as a specific instance? The answer's _both_, isn't it? My head hurts.)

- [!] Need to challenge the assumption that a spread's interpretation relies solely on the individual card meanings and their positions. While this is the foundation, there may be emergent or holistic meanings that arise from the interaction of cards, which the current attributes might not fully capture.

```Python
class Spread
    def __init__ # (self, ...)
    self.name = name # A string
    self.creator = creator # Enacting attribution as a value the program is keen on? Consider allowing for multiple creators or a more flexible attribution system.
    self.spread_type = spread_type # Not sure about this; an enumeration of predefined spread types, maybe (enumerations are immutable, but we could add to them?)
    self.spread_keywords = spread_keywords # ??? I guess querents might want to search or filter types of spread, but I don't want to reify a super-categorical approach
    self.spread_layout # A list of tuples, or a 2D array? (see also: visualisation, below) Consider how to handle irregular layouts, overlapping positions, or dynamic spreads that change based on certain conditions.
    self.reversals = reversals # As in, are they allowed? Random? User-defined? (Enums, or a Boolean?)
    self.positions = positions # A list of position objects representing the layout of the spread. Each position should have its own attributes like name and meanings (keywords, description?). Is a position an entity, rather than an attribute? A dictionary, or a list of tuples? Will positions always be named?
    self.cards = cards # A data structure (e.g., list or dictionary) to store the cards dealt into the spread; the core attribute that holds the spread's content; need to weight up the relative advantages/disadvantages of this being a list or a dictionary
    self.card_interactions = card_interactions # How to model interactions between cards based on their positions? Are we looking at interaction objects??? A matrix or graph-like data structure??? This attribute could capture the flow of energy or narrative between the cards, allowing for "better" interpretations.
    self.reading_history = reading_history # Accessing a list of readings using this spread type? Readings might be more closely associated with the querent, so it's worth considering whether this attribute belongs elsewhere

    # If this is also encompassing readings, and they're not seperate classes
    self.date = date # A string, or a DateTime object
    self.querent = querent # The querent attached to the reading; need to think about how we handle significators?
    self.context = context # How the hell do you turn context into an attribute/value pair, lol
    self.interpretation = interpretation # A string, or a seperate object class (the LLMs are suggesting we might want a confidence score, which is objectively hilarious)? I guess this is about mapping each card to its position, and doing the meaning-making and interpretive work
    self.visualisation = visualisation # Eventually piping this into a JSON Canvas format, that can be ingested by e.g.Obsidian/Kinopio/similar; very much "stretch goals"? Also explore SVG or HTML templates.
    self.related_spreads = related_spreads # Sure, but related _how_, exactly? List of spread ids, if we've got ids.

    # More speculative
    self.archetypal_patterns # Extracing all the archetypes in the spread, and doing a compare & contrast
    self.elemental_balance # Birds'-eye view of the balance of suits and elemental energies in the spread, and how they're distributed
    self.numerological_patterns # Looking for and storing/caching sets of similarly numbered cards, or sequential runs
    self.chorus = chorus # Putting all the `named_entities` (or similar) in a given spread into some kind of box and letting them slug it out
```

#### To-dos

- [ ] Instead of having a single `interpretation` attribute, consider breaking it down into multiple attributes or methods that capture different aspects of the interpretation process. At the moment, it's a bit "black-boxed."
- [ ] Rather than storing `card_interactions` directly in the `Spread` class, consider creating a separate `Interaction` class that encapsulates the logic for determining and interpreting card interactions. This could help keep the `Spread` class more focused and modular. The drawback, I guess, is that `card_interactions` occur in a particular, situated context? Any `card_interactions` attribute could lead to a "combinatorial explosion", making it computationally expensive to process. Think about ways to efficiently store and retrieve these interactions, possibly using caching or lazy evaluation. (how would permacomputing or "reconstrained design" handle this?)
- [ ] Consider incorporating more querent-centric attributes, such as `querent_goals`, `querent_reflections`, or `querent_feedback`, to capture the querent's evolving relationship with the spread and its interpretation.

### Edge cases or outliers

Incomplete spreads: A spread is interrupted, and not all cards are dealt. The `Spread` class should handle incomplete spreads gracefully, allowing for partial interpretations or the option to complete the spread later.

Interactive spreads: A spread that evolves based on querent input or additional card draws (as clarification/resolution?). The `Spread` class should support interactive spreads by allowing for dynamic updates to the `cards` and `position_meanings` attributes based on user interactions.

Overlapping cards: Think about the first two positions in the Celtic Cross spread. What covers what, and how do those cards relate? (Entanglement, coupling?)

## Example: Time & Tide Spread

A simple, previously non-existent three-card spread.

1. ANCHOR
2. TIDE
3. HORIZON