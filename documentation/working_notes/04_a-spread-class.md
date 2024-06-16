# Working Notes 4: Roughing Out a Spread Class

## "Yes, but what _is_ a spread?"

A _spread_, in tarot, is the specific layout or arrangement of cards used for a reading. It provides the structure and positions into which the cards are dealt. Each position in the spread has a predefined meaning or interpretation that contextualises the card placed there. (link with anthropologist Pascal Boyer on "ostensive detachment")

An externally supplied context, or scaffold for eliciting/isolating salient details of the situation or predicament? Like a thrown quadrat? A way of cutting through the noise? Forcing the querent/reader to do reparative work, working to bridge/align the pre-defined meanings of the cards and the pre-defined meanings of the positions. A question of combinatorics?

A _reading_, then, is the actual act of interpreting the cards dealt into a spread. It involves considering the meanings of the individual cards, their positions in the spread, and the relationships and patterns formed between them. A reading is the dynamic, emergent process of deriving insights from the static structure of the spread.

| Spread     | Reading          |
| :--------- | :--------------- |
| Structure  | Meaning          |
| Predefined | Emergent         |
| Layout     | Interpretation   |
| Potential  | Actualisation    |

## Prototoyping in-progress

The class design should consider the philosophical perspectives of embodying worldviews through structure (Bogost's procedural rhetoric) and facilitating fluid, emergent interpretations (Jodorowsky's approach).

The class should align with the chosen data model (likely an Entity-Attribute-Value or EAV model) to ensure flexibility and extensibility in representing card attributes and meanings. The class should also provide a "surface" or interface for the querent to interact with, aligning with our goals of enabling self-discovery and personal growth.

Need to think again about the difference between the `Spread` class and individual `Spread` object instances.

I think we're using a JSON-style format for card data, which the `Spread` class will need to interface with to access card meanings and interpretations.

(Note: The final version of the program will not handle randomisation or card drawing directly, requiring the use of a physical tarot deck by the querent.)

### Questions

- [?] Oh god what's the difference between a "spread" and a "reading"?
    - A reading would need to include `querent`, `question`, `date`, `reading_summary`, etc.
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

```Python
class Spread
    def __init__ # (self, ...)
    self.name = name # A string
    self.spread_type = spread_type # Not sure about this
    self.positions = positions # A list of position objects representing the layout of the spread. Each position should have its own attributes like name and meanings (keywords, description?). Is a position an entity, rather than an attribute?
    self.interpretations = interpretations # A dictionary, mapping each position to its meaning or interpretation?
    self.cards = cards # A data structure (e.g., list or dictionary) to store the cards dealt into the spread; the core attribute that holds the spread's content
    self.card_interactions = card_interactions # How to model interactions between cards based on their positions?

```

## Example: Time & Tide Spread

A simple, previously non-existent three-card spread.

1. ANCHOR
2. TIDE
3. HORIZON