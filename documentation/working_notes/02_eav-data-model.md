# Working Notes 2: Roughing Out a Data Model

## Introduction

 Considering an Entity-Attribute-Value (EAV) data model for this Python tarot-reading program, which is suited for entities with a large, varying set of attributes. Instead of having a fixed table structure with columns for each possible attribute, the EAV model stores data as rows with three main columns:

- **Entity**: The specific object/entity being described (e.g. each of the 78 cards of the tarot deck)
- **Attribute**: The property/characteristic being stored (e.g. name, arcanum, suit, keywords, meanings, archetypes, actions, characteristics)
- **Value**: The actual value for the attribute of that entity

The EAV model is useful when entities have a large, varying set of attributes, and new attributes need to be added dynamically, e.g. medical records with diverse patient data. However, the EAV model complicates querying and reporting due to necessary joins across tables. It also requires additional metadata tables to track attribute definitions. Compared to traditional models, it trades query performance for flexibility.

Our proposed EAV model uses JSON-like notation, with each card as an object with key-value pairs. This allows for a flexible and extensible schema, where new attributes can be added without modifying the underlying database structure.

## A Bogostian-Jodorowskian approach to data model prototyping

Taking Ian Bogost and Alejandro Jodorowsky as key influences, I aim to integrate their respective philosophies and works into this round of EAV data model prototyping, in an effort to derive some broader design principles.[^1]

The main goal is to create a data model that is both technically robust and philosophically/ontologically aligned with the spirit of tarot as a tool for self-discovery and personal growth. By stress-testing our understandings of these contrasting influences, we can strengthen the EAV model to better fulfil its intended purpose.

### Bogost

A "Bogostian" approach to data models focuses on core mechanics and processes over data storage. To extend this to the EAV model, we need to:

1. **Consider the essential operations and interactions required for a "meaningful" tarot reading**. Focus on how entities, attributes, and values interact systematically.

2. **Design the EAV model around key actions**, such as drawing cards from the deck, laying spreads, and interpreting meanings. Ensure the data structure facilitates these central procedures.

3. **Embrace constraints and limitations**. Intentionally limit the scope of the entities, attributes, and relationships represented in the model, as a way to force creative thinking about what is _actually_ essential.

4. **Incorporate a "clinamen"**[^2], an exemption from strict adherence to constraints, providing (limited) flexibility for querents to personalise or supplement the model. The model should be a guide, not a rigid prescription.

5. **Model interrelated objects**. View the EAV structure as a network of interconnected entity, attribute, and value objects that interact systematically, not just as abstract data types.

6. **Recognise that the EAV model and algorithms embody a specific philosophy**, a perspective on tarot and divination. Reflect on the ontology the model advances, and how interactions could shape quarents' beliefs.

7. **Approach data model prototyping as philosophical "carpentry"**. Engage directly with the core materials, implementing EAV prototypes in a "low-level" language to grapple with the core complexities. Cycle between implementing prototypes, reflecting on the results, and refining the design based on those insights.

Key parts of Bogost's work, here, are **procedural rhetoric**, the embrace of **Oulipian constraints**, and **philosophical carpentry**.

Bogost's approach suggests modeling the tarot as a network of interacting objects and processes. He sees objects as having hidden depths and dynamic interactions. Extending this to the tarot, the EAV model should allow for card meanings and relationships to shift based on context. Attributes could have open-ended or probabilistic values (YIKES) rather than fixed meanings. We will need to map out the EAV structure as a network of interconnected entity, attribute, and value objects that interact _systematically_, not just as abstract data types. The program should focus users on how card objects connect, constrain, and create meaning for each other, inviting exploration of their latent valences and hidden depths. In doing so, it will enable users to experience tarot as an emergent system of objects rather than just a human interpretive framework. Readings will be generative and context-dependent, rather than fixed or didactic.

Bogost's work on "_procedural rhetoric_" involves identifying processes and systems that exist in the real world and representing them in interactive digital form, so people can explore and learn about those systems through play. This means focusing on how the entities, attributes and values interact systematically, not just as abstract data types. In the context of an EAV model for a tarot-reading program, procedural rhetoric manifests in how the data model's structure and the algorithms processing it implement a specific perspective on tarot and divination. The model is not just a database, but a representation/model of a belief system or ontology. It becomes a kind of "writing machine" that generates meaning through its structure and constraints, and not just through the literal card definitions it contains.

So what kind of procedural rhetoric does this EAV model encode? Its structure and dynamics will represent certain ideas about the tarot. The key, here, is that the model itself, not just the written descriptions, visual design, or user interface around it, can make persuasive claims about tarot and how it works. **This might include:** which card attributes are included and excluded (and how they relate), the specific randomisation and procedural generation techniques used (if any[^3]), encoded "rules" about which cards or combinations are more or less significant.

An "_Oulipian_" approach seeks to use constraints and limitations productively. Bogost argues that restrictions are a necessary requirement for creativity and meaningful play (something that resonates with other project influences, from permacomputing and "Reconstrained Design"). So what are our relevant constraints and material limitations? Rather than aiming for maximum flexibility, should we intentionally limit the scope of entities, attributes and relationships represented in the model? Constraints can force us to address what is truly essential, fostering a greater awareness of the core elements and dynamics of the tarot. **Operationalising this might involve:** limiting the number of attributes per entity, restricting value types or ranges for certain attributes, or defining a fixed set of high-level entitity types (e.g. card, suit, number).

Philosophical "_carpentry_" proposes ways of doing philosophy through hands-on making, engaging directly with one's core materials and intervening in the world. In this context, this might mean starting by implementing EAV prototypes in a "low-level" language (what does this mean?), testing it with "real" readings, reflecting on how well it captures the meaningful aspects of tarot, and directly manipulating data structures to grapple with the core complexities and trade-offs in-play.

In sum: Bogost's approach suggests focusing on the core mechanics and processes the EAV model needs to enable, working within constraints, and engaging directly with the materials to prototype from the bottom up. The EAV structure enables a data-driven, object-oriented model of the tarot system. Each card becomes an object with a unique identity and set of behaviours emerging from its attribute-value pairs. A "Bogostian", OOO-inflected EAV model would shape the program as a carpentry project that embodies a philosophical stance through its data structure and interactions, not just a neutral information retrieval system.

### Jodorowsky

Alejandro Jodorowsky's approach to tarot emphasizes the interconnectedness and fluidity of meanings, viewing the tarot as a tool for self-discovery and personal growth. Jodorowsky sees the tarot as a "nomadic cathedral", with each card as an essential component of the whole. His methodology can be integrated into the EAV model to create a dynamic and evolving system that reflects tarot's rich symbolic and esoteric associations.

To capture these symbolic and esoteric associations, our data structure will need to support:

1. **Numerological associations**: The EAV model will need to capture numerological attributes for each card and defining relationships between cards that share numbers. For example, the Magician (I), Strength (XI), and The World (XXI) would be linked as different manifestations of the number 1.[^4]

2. **Elemental correspondences**: Jodorowsky associates each of the four suits (Wands, Cups, Swords, Pentacles) with a classical element (Fire, Water, Air, Earth) and sees their interactions as fundamental to tarot interpretation. Air and fire are seen as "active", earth and water as "passive", etc. etc. The EAV model should capture these elemental attributes for each suit, defining rules for how the elements interact.[^5]

3. **Fluid interpretations**: Allowing multiple, context-dependent values for card attributes, which need to be dynamic, open to evolution or reinterpretation. Enabling the querent to add new attributes reflecting personal associations (yes yes yes). Representing card meanings as probabilistic or open-ended rather than definitive. The model might weight different interpretations based on the specific question, spread position, or adjacent cards. Importantly, Jodorowsky views the cards not as having fixed meanings, but fluid interpretations that interact with the querent or reader's own intuition and life experiences. So he would build in flexibility for attributes to shift based on context, which is definitely what we're after.

In this, our programme's EAV model will need to:

- **Capture and represent complex relationships**: This might involve relational attributes, mapping tables, and dynamic interpretation algorithms. For example, relational attributes could link cards in narrative or thematic sequences, such as the "Fool's journey" depicted in the Major Arcana, the numerological progressions in the Minor Arcana, or interactions between suits. Algorithms would be able to traverse these relational links, generating contextual card meanings.

- **Support emergent meanings**: The open-ended nature of the EAV approach would support querents' continually adding (and refining?) attributes and values, reflecting/recording/encoding their emerging insights and associations. The model needs to accomodate null or empty values for many attributes (∅), reflecting Jodorowsky's view that a card's significance emerges through relational interactions, and not a rigid, categorical assignment of meanings. Some attributes may be undefined or inapplicable in certain contexts. The data model should accommodate this openness and ambiguity as a feature, not a bug, mirroring the tarot's ability to generate new meanings.

- **Balance structure and openness**: While the EAV model needs to provide a structured framework for tarot readings, it should also allow for fluid interpretations and personal growth. This balance can be achieved by defining core entities and relationships while permitting dynamic and context-dependent attribute values. The model should be designed as a _living framework_ that evolves through interaction, not a fixed structure. 

The ultimate goal of a "Jodorowskian" approach is to create a data model that can support the tarot's status as a "living mirror". As the querent adds their own insights and associations, the model becomes a personalised map of their tarot journey. Jodorowsky's approach suggests building flexibility into the EAV model to allow for shifting interpretations based on context, creating a dense semantic network reflecting the tarot's interconnectedness, and designing the data structure to facilitate personal growth and inspiration. For Jodorowsky, the EAV structure would become a dense semantic network reflecting the Tarot's interconnectedness. Less a static database than an evolving knowledge graph, with mapping tables and metadata to manage the resulting relational complexity. In this context, querying a card could activate a cascade (!) of associated meanings, based on its position in these relational structures. (and _this_ is the "nomadic cathedral" thing, I think)

### Bogost ⧉ Jodorowsky

#### Synergies

- **Embodying worldviews through structure**: Bogost argues that the very structure and rules of a computational system can express ideas and make arguments. Similarly, Jodorowsky sees the structure of the tarot deck itself, with its arcana and suits, as embodying an esoteric worldview. An EAV model informed by both approaches would embed (encode) a perspective on tarot and divination in its core entities, attributes and relationships.

- **Emergent meanings through interaction**: For Bogost, the persuasive power of procedural rhetoric emerges through the player's interaction with the rule-based system. Similarly, Jodorowsky emphasises the interaction between the tarot's symbolism and the reader's intuition in generating insights. An EAV model combining these ideas would enable fluid, emergent interpretations through the dynamic interaction of card data, spreads, and querent reflection.

- **Constraints for expression**: Bogost highlights how creative constraints in a computational system can facilitate meaningful expression. Jodorowsky works within the constraints of the tarot's traditional structure and symbolism to generate new associations and ideas. A data model embracing this principle would use the constraints of the 78 cards and their established attributes to inspire insight, not just as a limitation.[^6]

#### Conflicts/tensions

- **Procedural vs. associative**: Bridging procedural rhetoric and associative (intuitive?) leaps through the strict entities and attributes of an EAV model may be challenging, and could limit some of the free-form nature of Jodorowsky's "process" (lol).

- **Authorial intent vs. reader response**: Querent.py's EAV model will need to balance embedding/encoding a particular perspective with allowing for reader-generated insights and associations.

- **Computational logic vs. esotericism**: A need to navigate/reconcile the trade-offs between rational, formal structures and the numinous aspects of tarot practice.

## Overall summary/sales pitch

We're shooting for a kind of interactive, procedural "nomadic cathedral"; a data structure that through its design and constraints generates emergent and evocative meanings in dialogue (perhaps literally) with each individual querent. We want to enact the tarot's worldview procedurally; focusing, in particular, on the interplay of structure and openness.

The program could model the tarot system as a network of interacting object-entities (???), decentring the querent as one object among many. At the same time, we want to surface the rich symbolic resonances between cards, and using the system's semantic density to provoke, jostle, and interpellate the querent, eliciting self-reflection (yessssss).

Querent.py can use this model to provide querents with a grounding in the tarot's core concepts and patterns, while empowering them to discover their own unique interpretations and associations. Queries and algorithms can highlight connections across the structured entities, surfacing insights and creative readings. The program becomes a tool for both learning the tarot's constraints and exploring its fluid interpretive potential, synthesising Bogost's and Jodorowsky's approaches.

## Core design principles/criteria

| No. | Description                                                                     |
| --- | ------------------------------------------------------------------------------- |
| 1.  | **Embody/encode a philosophical stance**[^7]                                    |
| 2.  | **Facilitate fluid, emergent interpretations**                                  |
| 3.  | **Represent interconnectedness through a dense relational structure**           |
| 4.  | **Treat the (data) model as an interactive, expressive, meaning-making system** |
| 5.  | **Balance structure and openness**                                              |
| 6.  | **Design for transformation, not just information retrieval**                   |

## Trade-offs between expressiveness & technical performance

Probably going to be the main challenge, with multiple trade-offs to be made.

To capture the fluid interconnections of the tarot, the EAV model needs to represent complex relationships (numerological, elemental, archetypal, etc.) between cards. This might involve relational attributes, mapping tables, and/or dynamic interpretation algorithms. 

To align with Jodorowsky's participatory, evolutionary approach, and enable emergence and querent-supplied content, the model needs to support open-ended attribute values, user-defined attributes, and the accumulation of personal reflections over time. At the same time, Bogost's work on procedural rhetoric suggests the EAV design can make arguments about the nature of tarot, not just store data. The choice of entities, attributes, and their relations will be an expressive medium.

On the technical side, querying and aggregating data across EAV tables can be complex and inefficient compared to conventional schemas, requiring many joins. As the tarot data grows, the model may struggle to deliver responsive query times, especially for real-time, user-facing features (like the conversational interface we're angling for).

A lack of strict typing and data validation in EAV can lead to data quality issues, hampering the reliability and consistency of tarot interpretations, even in single-querent contexts. The combinatorial explosion (oh no) of possible tarot arrangements and interpretations enabled by an expressive EAV model may rapidly overspill feasible computational limits (even if it wasn't on a Raspberry Pi). Intelligent constraints and heuristics will be needed to surface meaningful patterns without excessive latency.

### Managing these trade-offs

With lots of people inhaling through their teeth (and shaking their head ruefully) at the prospect of an EAV data model, there's also the possibility of adopting a hybrid approach, using conventional schemas for stable, high-volume data and reserving EAV for truly dynamic domains. Card _definitions_, for example, could be conventionally modelled, with EAV for interpretations and user data.

Push computation from query-time to data ingestion-time where possible. Batch process tarot arrangements and surface key insights to users via caching, rather than computing on-demand. Let the expressive data accrue, and mine it asynchronously (lol).

Provide clear user guidance on the scope of dynamism and emergence in the model. Expose the philosophical tradeoffs in the UI, so users understand what is fixed vs. fluid. Make the EAV model's expressiveness a feature, not just an implementation detail (love this, yes).

Instrument fine-grained usage metrics to identify where expressive power is actually needed and valued. Progressively optimise performance based on empirical user behavior. _The EAV model should be as expressive as necessary, but no more._

## Examples:

### 0. The Fool

> "0 - The Fool": "Beginnings, innocence, spontaneity. The eternal child, filled with wonder and trust in the universe. Embarking on a new adventure with a free spirit and faith in the future."

```json
{
  "name": "0 - The Fool", // Split this into indexical ID number and name?
  "number": 0, // Maybe everything from here on in should be attributes, and a level down??
  "arcanum": "Major", // Which attributes should be singular, and which should be plural?
  "keywords": [ // The LLMs have supplied three keywords for each card, which is handy
    "Beginnings",
    "Innocence",
    "Spontaneity"
  ],
  "description": "The eternal child, filled with wonder and trust in the universe. Embarking on a new adventure with a free spirit and faith in the future.", // All of the LLM-supplied interpretation string, sans keywords
  "archetypes": "The eternal child", // Possible to have multiple archetypes, or none
  "named_entities": [ // Or depicted entities?
    "The eternal child", // The fool the guy, rather than "O - The Fool" the card
    "The universe", // In which the fool has wonder and trust
    "A new adventure"
  ],
  "actions": "Embarking on a new adventure", // Verbs, basically
  "emotions": [ // Ontologically trickier; how do emotions work?
    "innocence", // Is "innocent" an emotion?
    "wonder",
    "trust"
  ],
  "characteristics": [ // States or qualities, things that could be otherwise
    "innocent",
    "spontaneous",
    "eternal child",
    "free spirit",
    "faith in the future"
  ],
  "querent_notes": ""
}
```

### The Eight of Swords

> "The Eight of Swords": "Restriction, imprisonment, powerlessness. Feeling trapped by limiting beliefs. Avoiding responsibility for one's circumstances."

```json
{
  "name": "The Eight of Swords",
  "number": 8,
  "arcanum": "Minor",
  "suit": "Swords",
  "keywords": [
    "Restriction",
    "Imprisonment",
    "Powerlessness"
  ],
  "description": "Feeling trapped by limiting beliefs. Avoiding responsibility for one's circumstances.",
  "archetypes": null,
  "named_entities": null, // Or depicted entities? I'm guessing this isn't "eight swords"
  "actions": [
    "Feeling trapped", // Is this an action?
    "Avoiding responsibility",
  ],
  "emotions": "Feeling trapped", // Is this an emotion?
  "characteristics": [
    "restricted",
    "imprisoned",
    "powerless",
    "feeling trapped",
    "avoiding responsibility",
    "limiting beliefs" // What I really want is something like `"limiting_beliefs": True` (rofl)
  ],
    "querent_notes": ""
}
```

### The Knight of Pentacles

> "The Knight of Pentacles": "Reliability, hard work, productivity. The committed and responsible worker, steadily pursuing his goals with patience and determination. Bringing ideas into physical form through discipline."

```json
{
  "name": "The Knight of Pentacles",
  "arcanum": "Minor",
  "suit": "Pentacles",
  "court_card": true, // Does this make sense as a Boolean? Might be a better label for it, too.
  "rank": "Knight",
  "keywords": [
    "Reliability",
    "Hard work",
    "Productivity"
  ],
  "description": "The committed and responsible worker, steadily pursuing his goals with patience and determination. Bringing ideas into physical form through discipline.",
  "archetypes": "The committed and responsible worker",
  "named_entities": "The committed and responsible worker", // The knight of pentacles the guy, as opposed to "The Knight of Pentacles" the card?
  "actions": [
    "Steadily pursuing his goals",
    "Bringing ideas into physical form",
  ],
  "emotions": [
    "patience",
    "determinism"
  ],
  "characteristics": [
    "reliable",
    "hard-working",
    "productive",
    "committed",
    "responsible",
    "steady",
    "patient",
    "determined",
    "disciplined"
  ],  
  "querent_notes": ""
}
```

## Desmuntar

[^1]: (J) Also now thinking about this in relation to valuation studies, because of course.
[^2]: A "clinamen" is an inclination or deviation from an otherwise straight path; an unpredictable/spontaneous element introduced to an otherwise deterministic system.
[^3]: (J) For example, my (repeated) insistance that this program will not handle randomisation or card drawing, but/and require a physical tarot deck to use.
[^4]: (J) This will be important in, for example, representing and using numerical correspondences (multiples of the same number), or sequential runs.
[^5]: (J) Good for "distant reading" of a spread, i.e. if there's a massive heap of Minor Arcana from the wands suit, for example, that's probably important. At the same time, two of the same suit in close proximity might "amplify" each other.
[^6]: (J) We might also want to constrain the file size, in line with permacomputing etc.
[^7]: (J) We want to use the structure of the EAV model itself to make a procedural argument about how tarot "works"; the choice of entities, attributes and their relationships should reflect a coherent perspective.