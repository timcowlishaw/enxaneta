# Working Notes 2: Roughing Out an EAV Data Model

## Introduction

**Entities**: The 78 cards of the tarot deck, divided into 22 Major Arcana and 56 Minor Arcana.

**Attributes**: Various properties or characteristics associated with each card, such as name, number, arcanum, rank, suit, keywords, meanings, journey stage, outlook, emotions, actions, outcomes, characteristics, advice, archetypes, and entities (related cards).

**Values**: The actual data or content corresponding to each attribute for a given card.

The data model is structured using JSON-like notation, with each card represented as an object containing key-value pairs for its attributes. This allows for a flexible and extensible schema, where new attributes can be added without modifying the underlying database structure.

## Possible attributes (indicative, non-exhaustive list):

- Card Name (string)
- Card Number (0-21, Ace)
- Arcanum (Major/Minor)
- Rank (Ace, 2-10, Page, Knight, Queen, King)
- Suit (Cups/Pentacles/Swords/Wands)
- Keywords (2-3 strings)
- Meanings (array of strings)
- Journey Stage (string)
- Outlook (string)
- Emotions (string)
- Actions (string)
- Outcomes (string)
- Characteristics (string)
- Advice (string)
- Archetypes (string)
- Entities (array of entity references)
- Keywords (text)

## Bogostian-Jodorowskian approaches to EAV Modelling

Taking Ian Bogost, Alejandro Jodorowsky, and the Reconstrained Design Group as key influences on this undertaking, have spent a little bit of time working through how their respective philosophies and bodies of work would/could shape this stage of prototyping, in an attempt to derive some broader design principles. (Also thinking about this in relation to valuation studies, because of course.)

Ultimately, the goal is to synthesize these insights to create a data model that is both technically robust and philosophically/ontologically aligned with the spirit of tarot as a tool for self-discovery and personal growth. By stress-testing our understanding of these influences, we can refine the EAV model to better serve its intended purpose.

### Bogost

Unlike other EAV approaches, Bogost would focus on the core mechanics and processes rather than the data. Start by leaping ahead and considering the fundamental operations and interactions the EAV model needs to enable, rather than its data storage capacity. (a form of backcasting?)

Bogost's work on "procedural rhetoric" involves identifying processes and systems that exist in the real world and representing them in interactive digital form, so people can explore and learn about those systems through play.

Analysis of the kinds of entities, attributes, and relationships that exist in the problem domain the EAV system aims to capture. Working backwards from concrete, specific examples, as a prelude to abstraction?

Instead of starting with an exhaustive list of entities, attributes and values, consider the fundamental operations and interactions the EAV model needs to enable for a meaningful tarot reading experience. Work backwards from concrete examples of desired readings. This means focusing on how the entities, attributes and values interact systematically, not just as abstract data types.

Design the EAV model around the key actions users take when interacting with the tarot, such as drawing cards, laying spreads, and interpreting meanings. Ensure the data structure facilitates these core procedures.

An Oulipian approach, using constraints and limitations productively. Bogost argues that design constraints and material limitations, rather than total freedom, are a necessary precondition to creativity and meaningful play.
What are the relevant constraints and material limitations? (clear links here to the "Reconstrained Design" approach, and work on permacomputing) Rather than aiming for maximum flexibility, intentionally limit the scope of entities, attributes and relationships represented in the model. Constraints can force innovative thinking about what is truly essential.

**This might involve:** limiting the number of attributes per entity, restricting value types or ranges for certain attributes, or defining a fixed set of high-level entitity types (e.g. card, suit, number)

How can we allow for "clinamen"? A swerve from strict adherence to constraints, building in some (limited) flexibility for the user/querent to bend or break the constraints at times, enabling personalisation and serendipitous insights. The model should be a guide, not a rigid prescription.

Treat the data model itself as a kind of "writing machine" that generates meaning through its structure and constraints, not just through the literal card definitions it contains.

Thoughtfully chosen constraints can foster a greater awareness of the core elements and dynamics of tarot. They can enable a process of working through the essential aspects of a reading.

- [?] How can we _operationalise_ constraints? Limit attributes or force groupings to channel querent engagement?

Modelling the world in terms of interrelated objects; complex networks of objects and processes that interact with each other, not just the user/querent. Need to map out the EAV structure as a network of interconnected entity, attribute, and value objects that interact _systematically_, not just as abstract data types.

Bogost's OOO sees objects as having hidden depths and dynamic interactions. Applying this to tarot, the EAV model should allow for card meanings and relationships to shift based on context. Attributes could have open-ended or probabilistic values (YIKES) rather than fixed meanings. An OOO-inflected EAV model would shape the program as a carpentry project that embodies a philosophical stance through its data structure and interactions, not just a neutral information retrieval system. In doing so, it would enable users to experience tarot as an emergent system of objects rather than just a human interpretive framework.

The program would focus users on how card objects connect, constrain, and create meaning for each other, inviting exploration of their hidden depths and valences. Readings would be generative and context-dependent rather than fixed or didactic.

In the context of an EAV model for a tarot-reading program, procedural rhetoric manifests in how the data model's structure and the algorithms processing it implement a specific perspective on tarot and divination. The model is not just a database, but a representation/model of a belief system.

This might include:

- What card attributes are included and excluded, and how they relate (making an argument about meaning, value, importance)
- How querents are permitted/supported in generating readings or spreads, enacting a particular method of tarot use
- Randomisation and procedural generation techniques used in dealing and reading generation express ideas about chance, fate, and the role of human/computer agency (e.g. my insistence that this will eventually require a physical deck to use)
- Any encoded rules about what card combinations are more or less significant make claims about how tarot meaning emerges from card interaction (e.g. Major Arcana being more powerful or dominant, less quotidian?)

What kind of procedural rhetoric does this EAV model embody or encode? Representing and reifying certain ideas about the tarot, tacitly or explicitly, through its structure and dynamics. Bogost would encourage reflecting on what worldview the model advances, and how interaction with it could shape users' beliefs. The key, here, is that the model itself, not just the written descriptions, visual design, or user interface around it, can make persuasive claims about tarot and how it works. 

We're looking at a dense network of interconnected objects (cards) with attributes emerging from their positions and relations. Bogost would focus on the system's behaviors over its raw data.

Prototyping from the bottom up, engaging directly with the core materials. Prototyping, as "carpentry", becomes a form of applied philosophy. Could start implementing EAV prototypes in a "low-level" language (what does this mean?), directly manipulating data structures to grapple with the core complexities.

Cycle between implementing EAV prototypes and reflecting on how that practical experience reshapes your conceptual models, allowing each to inform the other. Carpentry involves a cycle of hands-on making, stepping back to reflect on the results, and then refining the design. For the tarot program, this could mean implementing a basic EAV model, testing it with real readings, reflecting on how well it captures the meaningful aspects of tarot, and then evolving the model based on those insights.

The EAV structure enables a data-driven, object-oriented model of the tarot system. Each card becomes an object with a unique identity and set of behaviours emerging from its attribute-value pairs. Bogost would likely see this as a starting point for procedurally expressing the inner workings of the Tarot in software.

> Bogost's approach suggests focusing on the core mechanics and processes the EAV model needs to enable, working within constraints, and engaging directly with the materials to prototype from the bottom up.

### Jodorowsky

For Jodorowsky, the main entities would be the 78 cards of the tarot deck itself: the 22 Major Arcana and 56 Minor Arcana. He sees the tarot as a "nomadic cathedral", with each card as an essential component of the whole.

The data model should try to capture this interconnectedness, perhaps through relational attributes linking cards or metadata mapping higher-order structures.

The goal is to sustain the tarot as a "living mirror", evolving with the querent. As the they add their own insights and associations over time, the model becomes a personalized map of their tarot journey.

Jodorowsky goes hard on numerology, elemental correspondences, and other esoteric associations. His approach to the Minor Arcana of the TdM deck, in particular, leans more on the interactions of the numerological and elemental (suit) associations. (this symbolic richness is something I'm less interested in and/or worried about, but is important in handling the Minor Arcana of the TdM, as I understand it)

**Numerological associations**: In the EAV model, this suggests capturing numerological attributes for each card and defining relationships between cards that share numbers. For example, the Magician (I), Strength (XI), and The World (XXI) would be linked as different manifestations of the number 1. (this is important in, for example, capturing numerical correspondences (multiples of the same number), or sequential runs)

**Elemental correspondences**: Jodorowsky associates each of the four suits with a classical element (Wands-Fire, Cups-Water, Swords-Air, Pentacles-Earth) and sees their interactions as fundamental to interpreting the cards. Air & fire as "active", earth and water as "passive", etc. etc. The EAV model should capture these elemental attributes for each suit and define rules for how the elements interact. (if there's a massive heap of wands in a given spread, for example, that's probably important; two of the same suit might amplify each other)

Supporting "fluid interpretations", by:

- Allowing multiple, context-dependent values for card attributes
- Enabling the querent to add new attributes reflecting personal associations (yes yes yes)
- Representing card meanings as probabilistic or open-ended rather than definitive

Importantly, Jodorowsky views the cards not as having fixed meanings, but fluid interpretations that interact with the querent or reader's own intuition and life experiences. So he would build in flexibility for attributes to shift based on context, which is definitely what we're after.

The model might weight different interpretations based on the specific question, spread position, or adjacent cards. (a gesture towards reparative reading, which is something we can, I think, let the language models loose on)

Thinking about relationships, relational attributes? Examples might include the journey of the Major Arcana, the numerological progressions in the Minor Arcana, and the thematic interactions between suits. Values specifying other related cards (as entities)?

What we're looking for is: Numerological, elemental, and other attributes for each card. Relational attributes linking cards in narrative or thematic sequences. Mapping tables or metadata capturing the higher-order structures like elemental dignities or the Fool's journey. Algorithms that traverse these relational links to generate contextual card meanings.

In this context, querying a card could activate a cascade (!) of associated meanings, based on its position in these relational structures. (and _this_ is the "nomadic cathedral" thing, I think)

For Jodorowsky, the EAV structure would become a dense semantic network reflecting the Tarot's interconnectedness. Mapping tables and metadata would manage this relational complexity.

He would likely allow for null or empty values for many attributes (∅), reflecting his view that a card's significance emerges through relational interactions, not in a rigid, categorical assignment of meanings. Some attributes may be undefined or inapplicable in certain contexts. The data model should accommodate this openness and ambiguity as a feature, not a bug, mirroring the tarot's ability to generate new meanings. (how is this handled in an EAV model?)

Data model as a _living framework_, not a fixed structure. In this, the open-ended nature of the EAV approach supports querents' continually adding (and refining?) new attributes and values, reflecting/recording/encoding emerging insights and associations.

Less a static database than an evolving knowledge graph. 

How to handle the trade-offs between expressiveness and technical performance?

Aiming for:

- Wholeness and interconnectedness (each card an essential part of the whole; is this the "gestalt" thing?)
- Layered meanings (what does this _mean_; I'm imagining filo pastry in way that's probably not helpful)
- Fluidity (the attribute values may need to be dynamic, open to reinterpretation)
- Transformative power (the data structure should be geared to facilitate personal growth and inspiration, not just a "view-from-nowhere" analysis; it should _interpellate_ the querent)
- Aesthetic symbolism (data structure needs to respond to the illustrations, symbolism, aesthetics of the cards; which is kind of tricky if we're (currently, at least) working to an average of different deck types)

> Jodorowsky's approach suggests building flexibility into the EAV model to allow for shifting interpretations based on context, creating a dense semantic network reflecting the tarot's interconnectedness, and designing the data structure to facilitate personal growth and inspiration.

### Bogost ⧉ Jodorowsky

#### Synergies

- **Embodying worldviews through structure**: Bogost argues that the very structure and rules of a computational system can express ideas and make arguments. Similarly, Jodorowsky sees the structure of the tarot deck itself, with its arcana and suits, as embodying an esoteric worldview. An EAV model informed by both approaches would embed (encode) a perspective on tarot and divination in its core entities, attributes and relationships.

- **Emergent meanings through interaction**: For Bogost, the persuasive power of procedural rhetoric emerges through the player's interaction with the rule-based system. Likewise, Jodorowsky emphasises the interaction between the tarot's symbolism and the reader's intuition in generating insights. An EAV model combining these ideas would be designed to enable fluid, emergent interpretations through the dynamic interaction of card data, spreads, and user reflection.

- **Constraining for expression**: Bogost highlights how creative constraints in a computational system can facilitate meaningful expression, not just limit it. Jodorowsky works within the constraints of the tarot's traditional structure and symbolism to generate new associations and ideas. An EAV model embracing this principle would use the constraints of the 78 cards and their established attributes to inspire insight, not just as a limitation. (might we also want to constrain the file size, in line with permacomputing etc.?)

#### Conflicts/tensions

- **Procedural vs. associative**: Bridging procedural rhetoric and associative (intuitive?) leaps through the strict entities and attributes of an EAV model may be challenging, and could limit some of the free-form nature of Jodorowsky's "process" (lol).

- **Authorial intent vs. reader response**: Querent.py's EAV model will need to balance embedding/encoding a particular perspective with allowing for reader-generated insights and associations.

- **Computational logic vs. esotericism**: A need to navigate/reconcile the trade-offs between rational, formal structures and the numinous aspects of tarot practice.

#### Admixtures/blends

- **Oulipics ⇆ fluid interpretations**: Defining "fixed" core entities and relationships (as the constraints within which fluid interpretations can emerge), but allowing for open-ended attribute values and user-generated attributes.Using constraints to highlight patterns. Balancing predefined and emergent meanings. Treating the data model itself as an expressive medium (!).

- **OOO ⇆ dense semantic network**: Treating each tarot card as an object with withdrawn potential, in Bogostian terms, only partially revealed through its attributes and relationships; but modeling the tarot system as a _dense relational network_. Tracking inter-object resonances (elemenetal conflict, archetypal reinforcements)? Modeling the querent as an object among objects (YIKES, but there's often a card to represent the querent, right?). Generating provocative questions and prompts for the user to reflect on, extending the reading beyond the immediate session in a sustained dialogue.

## Overall summary/sales pitch

We're shooting for a kind of interactive, procedural "nomadic cathedral"; a data structure that through its design and constraints generates emergent and evocative meanings in dialogue (perhaps literally) with each individual querent. Procedurally enacting tarot's worldview, in particular, this interplay of structure and openness.

The program could enact OOO (???) by modeling the tarot system as a network of withdrawn yet interacting object-entities (???), decentring the querent as one object among many. At the same time, it would realize Jodorowsky's vision by surfacing the rich symbolic resonances between cards, and using this semantic density to provoke, jostle, and interpellate the querent, eliciting self-reflection.

Querent.py can use this model to provide querents with a grounding in the tarot's core concepts and patterns, while empowering them to discover their own unique interpretations and associations. Queries and algorithms can highlight connections across the structured entities, surfacing insights and creative readings. The program becomes a tool for both learning the tarot's constraints and exploring its fluid interpretive potential, synthesising Bogost's and Jodorowsky's approaches.

## Core design principles/criteria

> 1. **Embody/encode a philosophical stance**[^1]
> 2. **Facilitate fluid, emergent interpretations**
> 3. **Represent interconnectedness through a dense relational structure**
> 4. **Treat the (data) model as an interactive, expressive, meaning-making system**
> 5. **Balance structure and openness**
> 6. **Design for transformation, not just information retrieval**

## Trade-offs between expressiveness & technical performance

Probably going to be the main challenge, with multiple trade-offs to be made.

To capture the fluid interconnections of the tarot, the EAV model needs to represent complex relationships (numerological, elemental, archetypal, etc.) between cards. This might involve relational attributes, mapping tables, and/or dynamic interpretation algorithms.

To align with Jodorowsky's participatory, evolutionary approach, and enable emergence and querent-supplied content, the model needs to support open-ended attribute values, user-defined attributes, and the accumulation of personal reflections over time.

At the same time, Bogost's concept of procedural rhetoric suggests the EAV design can make arguments about the nature of tarot, not just store data. The choice of entities, attributes, and their relations will be an expressive medium.

On the technical side, querying and aggregating data across EAV tables can be complex and inefficient compared to conventional schemas, requiring many joins. As the tarot data grows, the model may struggle to deliver responsive query times, especially for real-time, user-facing features.

A lack of strict typing and data validation in EAV can lead to data quality issues, hampering the reliability and consistency of tarot interpretations, even in single-querent contexts. The combinatorial explosion of possible tarot arrangements and interpretations enabled by an expressive EAV model may exceed feasible computational limits. Mitigations like partial indexes, materialized views, and ETL checks add development overhead. Intelligent constraints and heuristics will be needed to surface meaningful patterns without excessive latency.

### Managing these trade-offs

With lots of people inhaling through their teeth at the prospect EAV data models, there's the possibility of adopting a hybrid approach, using conventional schemas for stable, high-volume data and reserving EAV for truly dynamic domains.Card definitions, for example, could be conventionally modeled, with EAV for interpretations and user data.

Aggressively index EAV tables on commonly filtered attributes and pre-materialize frequent aggregation patterns.Judicious denormalisation can also accelerate query performance in exchange for update overhead and storage.

Push computation from query-time to data ingestion-time where possible. Batch process tarot arrangements and surface key insights to users via caching, rather than computing on-demand. Let the expressive data accrue, and mine it asynchronously (lol).

Provide clear user guidance on the scope of dynamism and emergence in the model. Expose the philosophical tradeoffs in the UI, so users understand what is fixed vs. fluid. Make the EAV model's expressiveness a feature, not just an implementation detail (love this, yes).

Instrument fine-grained usage metrics to identify where expressive power is actually needed and valued. Progressively optimise performance based on empirical user behavior. _The EAV model should be as expressive as necessary, but no more._

## Examples:

### 0. The Fool

> "0 - The Fool": "Beginnings, innocence, spontaneity. The eternal child, filled with wonder and trust in the universe. Embarking on a new adventure with a free spirit and faith in the future."

```json
{
  "name": "0 - The Fool",
  "number": 0,
  "arcanum": "Major", // Which attributes should be singular, and which should be plural?
  "keywords": [ // The LLMs have supplied three keywords for each card, which is handy
    "Beginnings",
    "Innocence",
    "Spontaneity"
  ],
  "description": "The eternal child, filled with wonder and trust in the universe. Embarking on a new adventure with a free spirit and faith in the future.", // All of the LLM-supplied interpretation string, sans keywords
  "archetypes": "The eternal child", // Possible to have multiple archetypes, or none
  "named_entities": [
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
}
```

### The Eight of Swords

> "The Eight of Swords": "Restriction, imprisonment, powerlessness. Feeling trapped by limiting beliefs. Avoiding responsibility for one's circumstances."

```json
{
  "name": "The Eight of Swords",
  "number": 8,
  "arcanum": "Minor",
  "keywords": [
    "Restriction",
    "Imprisonment",
    "Powerlessness"
  ],
  "description": "Feeling trapped by limiting beliefs. Avoiding responsibility for one's circumstances.",
  "archetypes": null,
  "named_entities": null, // I'm guessing this isn't "eight swords"
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
}
```

### The Knight of Pentacles

> "The Knight of Pentacles": "Reliability, hard work, productivity. The committed and responsible worker, steadily pursuing his goals with patience and determination. Bringing ideas into physical form through discipline."

```json
{
  "name": "The Knight of Pentacles",
  "arcanum": "Minor",
  "court_card": true, // Does this make sense as a Boolean? Might be a better label for it, too.
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
  ]
}
```

## Desmuntar

[^1]: We want to use the structure of the EAV model itself to make a procedural argument about how tarot "works"; the choice of entities, attributes and their relationships should reflect a coherent perspective.