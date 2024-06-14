# Working Notes 1: Modelling Tarot Reversals

In basic terms, I'm currently grappling with how to model card reversals in this weird little shonky tarot-reading prototype Python programme I've been working on. With the Tarot de Marseille as my main go-to, for now, I _think_ I only want reversals to apply to cards in the Major Arcana, based on it being difficult to discern the orientation of the "pips" of the Minor Arcana.

I'm leaning towards a `Card` object class, as something that supports some of my other plans, and will (I think?) enable tracking and analysis (e.g. percentage of reversed cards in a given spread, different cards' orientations over time). That said, I'm keen to avoid accidentally painting myself into a corner, and want to make sure I haven't overlooked any obvious issues or drawbacks.

Keen to encode Jodorowsky's philosophy into the procedural rhetoric of the model, defaulting to open-ended questions and prompts that encourage self-reflection when a reversal appears, rather than definitive statements. Guide the querent to find their own meaning.

## "Yes, but what _is_ a reversal?"

Reversed cards in a reading are a result of blind shuffling.

Rather than just a upright/reversed binary, reversals gesture to a spectrum of interpretive meanings for each card. A reversal can indicate the energy of the card is blocked, turned inwards, early or late in its appearance, or manifesting in a more challenging or "shadow" form.

I'm interested in modelling reversals in a way that is less about opposition or negativity, and more about a card's _latency_, or hidden properties (blockages, delays, etc.).

It's also about the _relationship_ between reversed and upright cards. If lots of cards are upright, the few reversals stand out more, and vice versa.

A reminder that situations and energies are not fixed or static, but constantly shifting.

Ways to see through to "the other side", going beyond the limits of the known?

A realm of potentials and underlying causes. All a bit subjunctive?

ADDING NUANCE. (though: cf. Kieran Healy, "Fuck Nuance")

If the upright card represents one set of attributes, a reversal is one of multiple possible lenses transforming that set. The interpretive challenge is in figuring out which transformations should be applied.

Contextual analysis, querent input.

Adversity, challenge, tests of character?

From an OOO perspective, rather than simply inverting or negating the card's upright meaning, the reversal could be seen as activating _a different set of capacities_ within the card-object. The reversed position doesn't merely flip the meaning, but reconfigures the card's internal composition and its relations to the other cards in the spread.

The reversal reshapes the relational field, opening up new lines of interpretation and insight. From this view, the choice to read reversals or not is less about technical proficiency or interpretive sophistication, and more about the reader's orientation to the cards as meaning-making objects. Reading reversals could be seen as a way of _attending to the hidden depths and alternative potentials lurking within each card_ - an invitation to explore the "strange stranger" that withdraws behind the card's surface meanings.

Reversals as a negation or inversion of a card's core attributes or base meanings? Each card contains within itself both upright and reversed meanings, with the reversal acting as a switch or selector between these two sets of potentials.

James Ricklef's "Five Ds": 1. _Delay_ of the original effect; 2. _Diminuation_ of the original effect; 3. _Direct opposite_ of the original meaning; 4. _Dark side_ of the original meaning; 5. _Direction change_.

> 'Problems ... represent energy that is constrained and can be liberated.' (Greer 2002)

> 'Since both upright and reversed images are part of the card's energy, its full range is there for you to access, but it may feel like jumping a hurdle or walking through molasses.' (Greer 2002)

> 'Consider what the words `REVERSAL`, `UPSIDE-DOWN`, `TOPSY-TURVEY`, `TURNED AROUND`, `INVERTED` mean to you.' (Greer 2002)

> 'In general, it helps to think of reversed cards as "red flagged," indicating that you should pay extra attention to them. They signal that something is not operating as usual. Upright cards tend to be conscious, outer, automatic, in process, and available. Reversed cards often indicate choice points, where you must be attentive. They may require conscientious, willful handling if you are to take full advantage of the energies and opportunities. It is like knowing that a car has a tendency to pull to the right and so you have to keep alert and make adjustments for it. Or they are places to stop struggling, relax, and let go of all expectations.' (Greer 2002: 25)

- [!] _The Hanged Man_ itself epitomises the nature of reversed cards, so take this as our guide or heuristic.

## 12 main ways to read reversals (after Greer 2002); of which the following 10 are relevant to us:

### 1. **Blocked, Resisted**

> 'The energy normally described by the card may be blocked, repressed, denied, rejected, or resisted.' (Greer 2002)

[Obstacles, hindrances, and resistance to the card's energy.]

In an object-oriented `Card` class model, this could be represented through a `reversed` boolean attribute that, when `True`, triggers an alternate set of meanings or interpretations associated with blockage or resistance. These alternate meanings could be stored as additional attributes on the Card object, such as `blocked_meaning` or `resisted_archetype`, paralleling the standard `meaning` and `archetype` attributes.

_Alternatively_, the `Card` class could include methods like `meaning()` and `archetype()` that return different values based on the state of the reversed attribute, encapsulating the reversal logic.

In a procedural model like a tuple `(card, reversed)`, this negation operation could be applied when the `reversed` boolean is `True`, perhaps via a function like `apply_reversal(meaning)` that takes a base meaning and returns its negated or inverted form.

(These two approaches are essentially equivalent, right?)

The negation operation could involve a variety of procedural techniques, such as:

- Retrieving antonyms or semantic opposites of key terms in the base meaning (from where?)
- Applying negative modifiers or prefixes to key phrases, e.g. "Lack of...", "Inability to...", "Resistance to..."
- Searching for pre-defined reversed meanings associated with the card in a tarot interpretation database
     
Procedurally, applying this technique would involve an additional step in the interpretation process, where the reversal status of each card is checked and the appropriate negation or inversion operation is applied to generate the final reversed meaning. This additional reversal step could be encapsulated in the `Card` class methods or in standalone functions, depending on the overall architecture of the program. 

["Blocked", "Stuck", "Stymied", "Thwarted", "Struggled with", "Denied", "Avoided", "Defied", "Resisted", "Repressed", "Refused", "Rejected"]

This list of keywords could be used to generate or retrieve these alternate reversed meanings, perhaps via a pre-trained language model or semantic search against a corpus of tarot interpretations. (???)

Interpreting a spread with multiple reversed cards would involve repeatedly applying this negation procedure to each card's base meanings, then synthesising the results into a coherent interpretation. Tracking the history of a card's reversals over multiple readings could yield interesting insights into patterns of blockage or resistance over time, perhaps suggesting areas for deeper introspection or growth for the querent.

### 2. **Projected**

> 'There could be a tendency to project denied material onto others. These may be qualities you admire as well as those you do not like.' (Greer 2002)

[Psychological mirroring, reflecting denied or disowned aspects of the self.]

**Summary**: Reversals as a kind of psychological mirror, reflecting aspects of the self that are denied or disowned. Each card contains within itself a set of potential projections: qualities that we may see in others but fail to recognise in ourselves. The reversal acts as a kind of flip, _turning the card's energy outward_ rather than inward. Procedurally, the interpretation of a reversed card should involve a kind of psychological mirroring or reflection process, where the qualities of the card are examined as potential projections of the querent.

In an object-oriented Card class model, this could be represented through a `projected_attributes` property that holds an array of qualities associated with the card when reversed. These attributes would be distinct from the card's core `attributes`, representing a shadow or denied aspect of the self. The `projected_attributes` could include both positive and negative traits. For example, the reversed King of Wands might have projected_attributes like `["confident", "arrogant", "passionate", "impulsive"]`.

In a procedural model, this could involve a `project_attributes(querent)` method on the `Card` class that compares the `projected_attributes` to the `querent` object's own attributes (!!!), looking for matches or discrepancies. This method could return a interpretation string highlighting any projections. 

Procedurally, applying this technique would involve an additional step in the interpretation process, where each reversed card is examined for potential projections based on the querent's psychological profile. This profile could be gathered through an initial intake form (!!!) or dynamically throughout the reading.

["Projected"]

### 3. **Delayed, Difficult, Unavailable**

> 'There could be hesitation, uncertainty, unavailability, or an external delay. With many cards reversed, overall change may take longer that expected.' (Greer 2002)

[Temporal challenges, delays, and difficulties in manifesting the card's energy.]

**Summary**: Reversals as modifiers of the card's temporal unfolding or accessibility, rather than negations of its fundamental meaning. Each card contains latent potentials that may be delayed, made difficult, or rendered temporarily unavailable by a reversal. The reversal doesn't negate the card's core meaning, but rather modifies the ease and timeline of its manifestation. The querent's actions and choices can impact the degree of delay or difficulty, with 'negative' reversals as temporary challenges rather than permanent, immutable obstacles.

This framing implies that the querent's actions and choices can impact the degree of delay or difficulty, and that 'negative' reversals may be temporary challenges rather than permanent, immutable obstacles. The data model could reflect this by allowing reversal attributes to be updated based on the querent's evolving context.

In an object-oriented `Card` class model, this could be represented through attributes like `delay`, `difficulty`, or `availability`, which could hold values indicating the degree or nature of the impediment (lol).

Reversal attributes could be set based on the specific reversal keyword, e.g., `card.set_reversal('delay', 'Hesitated')`, allowing for nuanced descriptions of the blockage.

In a procedural model, this could involve applying functions like `delay()`, `make_difficult()`, or `make_unavailable()` to the card's upright meaning, based on the specific reversal keyword.

The interpretation could also suggest potential actions or choices the querent could make to overcome the delay or difficulty, based on the specific nature of the blockage. For example, a "Hesitated" reversal might prompt the querent to examine and overcome their indecision, while an "Obstructed" reversal might suggest identifying and removing external barriers.

In a multi-card spread, the presence of multiple reversals with delay or difficulty keywords could suggest a slowdown in the querent's progress or development. The program could track the frequency and severity of such reversals across readings to identify persistent patterns of blockage.

["Delayed", "Hestitated", "Held back", "Set back", "Made difficult", "Rough road", "Indecisive", "Distracted", "Obstructed", "Hindered", "Suspended", "Inhibited", "Turned away from"]

### 4. **Inner, Unconscious, Private**

> 'The energy might be unconscious, inner, or private rather than conscious, outer, or public.' (Greer 2002)

[Internal, hidden, or unconscious aspects of the card's energy.]

**Summary**: Reversals as pointers to the querent's inner world, in contrast to the outer, public face represented by upright cards. The technique maps the tarot system onto a model of the psyche, with upright cards representing conscious phenomena and reversals representing the unconscious. Procedurally, interpreting a reversed card as "inner, unconscious, private" involves a kind of psychological mirroring or reflection, where the card's energy is understood as an internal state or process of the querent.

In an object-oriented `Card` class model, this could be represented through a `facing` attribute with values like `"upright"`, `"reversed"`, `"inner"`, `"outer"`, etc. The facing would indicate the ontological status of the card's energy - whether it manifests internally or externally. Alternatively, a `reversed_meaning` attribute could hold interpretations specific to the inner/unconscious reading, distinct from the upright meaning. This separates the two ontological realms. (I think this is too binary?)

In a procedural model, this could involve functions like `interiorise()` or `reflect()` that transform the card's upright meaning into a statement about the querent's inner world, e.g., `interiorise("Creative abundance")` yields `"In your inner world, creative abundance"`.

["Inner", "Inward", "Unconscious", "Internal", "Personal", "Private", "Deep", "Secret", "Covert", "Unexpressed", "Indirect", "Underground", "Underlying", "Concealed", "Unseen", "Beneath", "Below"]

### 5. **Breaking Through, Overturning, Refusing, Changing Direction**

> 'The querent could be overturning, getting out from under, breaking free of, rejecting, refusing, or turning away from the condition pictured. It can also show the end of passing away of a situation, a loosening, or a change in direction.' (Greer 2002)

[Transformative thresholds, pivotal choice points, and active change.]

**Summary**: Reversals as transformative thresholds or pivotal choice points. Ontographically, this frames the tarot reading as a space of potential transformation, where each reversed card is a fork in the path, inviting the querent to overturn old patterns or change direction. Reversals mark points of instability where new possibilities can emerge through the querent's active choices. Procedurally, interpreting a reversal as "breaking through" or "changing direction" involves identifying the querent's current relationship to the upright meaning, and then signaling a potential point of departure or transformation.

This technique aligns with an ontology of becoming and emergence, where the querent's engagement with the cards' energies is fluid and dynamic. The spread maps a landscape of thresholds and pivotal moments. Reversals mark points of instability where new possibilities can emerge through the querent's active choices (yesssss). Philosophically, it resonates with ideas of radical freedom and self-creation, framing the querent as an agent actively shaping their path, not just passively receiving the cards' meanings. The reversal is an invitation to overturn determinism.

In an object-oriented model, this could be represented through a `reversed_action` attribute on the Card class, holding values like `"overturning"`, `"breaking free"`, `"rejecting"`, `"turning away"`, etc. This attribute signifies the querent's active stance towards the card's energy.

In a procedural model, this could involve functions like `assess_relationship()` and `propose_reversal()` that analyse the querent's situation and suggest potential reversed meanings.

Applying this technique would involve first calling `assess_relationship()` to diagnose the querent's current state, then feeding that into `propose_reversal()` to generate the specific reversal interpretation, e.g. "breaking free from limitation". The reading becomes a springboard for embodied change.

["Overturned", "Overthrown", "Overcome", "Broken through", "Put down", "Changed", "Adjusted", "Toppled", "Out from under", "Falling away", "Unseated", "Breached", "Loosened", "Freed", "Released"]

### 6. **No or Not (the upright meaning); Lacking**

> 'Occasionally you can preface a standard upright interpretation with "no" or "not." Or try adding prefixes such as "non-" or "un-" to upright meanings. ... Take care that this does not lead to a judgemental, overly deterministic, or negative attitude.' (Greer 2002)

[Binary negation or absence of the card's core qualities.]

**Summary**: Reversals as a kind of binary switch, toggling between the presence and absence of a card's core qualities. Each card's meaning oscillates between its upright significance and its negation, with no intermediate states. The reversal flips the card's polarity. Procedurally, interpreting a reversal as "No or Not (the upright meaning)" involves a straightforward negation operation. Perhaps best understood as a kind of "ground level" of reversal, a _first approximation_ of the card's inverted meaning that sets the stage for deeper, more individualised interpretations to emerge, in dialogue with the querent. A practical entry point to begin grappling with the tarot's inverted meanings.

Ontographically, this technique maps the tarot's symbolic world onto a binary space of presence and absence. (However, this binary ontology risks reducing the tarot's symbolic richness to a series of on/off switches, losing sight of more subtle shades of significance.)

In an object-oriented `Card` class model, this could be represented through a reversed boolean attribute. When `True`, the card's meaning would be interpreted as the negation of its upright attributes.

Procedurally, the program would prepend "No" or "Not" to the card's upright meaning, or add negating prefixes like "non-" or "un-" to key terms. In a procedural model, this could be implemented as a `negate()` function that takes the upright meaning string and returns its negated form.

Applying this technique would involve checking the `reversed` attribute of each card and, if `True`, passing its `upright_meaning` through the `negate()` function to generate the reversed interpretation. This negation operation could be extended with more sophisticated natural language processing techniques, such as identifying and negating key sentiment words or phrases within the upright meaning. (However, as Greer cautions, this mechanical negation risks generating interpretations that are overly machinic or pessimistic. The program may need to incorporate additional heuristics to maintain a balanced perspective.)

The program could also track the frequency of negated interpretations across a reading and provide compensatory prompts for reflection if they exceed a certain threshold, to avoid an overly negative tone (rofl).

["No", "Not", "Negated", "Inverse of", "Lacking", "Absent", "Without", "Ended", "End of", "Discontinued"]

### 7. **Excessive, Over- or Undercompensating**

> 'The reversal may intensify or lessen the meaning of the card, or take it to extremes and overindulgence: too little or too much, under or overdeveloped, immature or senile. In pyschological terms it can indicate over- or undercompensation, or a tendency to flip dramatically between polarities.' (Greer 2002)

[Spectrum of intensity, over- or under-expression of the card's energy.]

**Summary**: Reversals as a spectrum of intensity, rather than a binary state. Ontographically, it frames the tarot reading as a landscape of energetic intensities, with each card manifesting its archetypal meaning to a greater or lesser degree. The spread becomes a map of imbalances and compensations (_nice_). This aligns with an ontology of the psyche as a dynamic system seeking equilibrium. Reversals represent over- or under-compensations in that system, pointing to areas of excessive or deficient expression. Procedurally, interpreting a reversal as "excessive" or "deficient" involves scaling the intensity of the card's core meaning up or down, based on the degree of reversal.

In an object-oriented `Card` class model, this could be represented through an intensity attribute, perhaps an integer or enum type, indicating the degree of over- or under-expression of the card's energy.

In a procedural model, this could involve functions like `intensify()` or `diminish()` that modify the card's upright meaning based on its intensity attribute. Applying this technique would involve setting the `intensity` attribute of reversed cards, then calling the `interpret()` function to generate the modified meaning.

The interpretation could suggest reflections or actions to bring the energy into balance, based on whether it is excessive or deficient. For example, an excessively assertive King of Wands might prompt the querent to practice humility and collaboration (lol).

In a multi-card spread, the program could analyze the overall balance of intensities, highlighting areas of overcompensation or deficiency in the querent's life. It could suggest practices to harmonise these energies.
Over a series of readings, the program could track the querent's progress in balancing the energies of frequently reversed cards, offering guidance and affirmation.

["Too much", "Too strong", "Overwhelmed", "Overly", "Excessive", "Exaggerated", "Intensified", "Overindulged",  "Ungrounded", "Out of control", "Tentative", "Toned down", "Softened", "Embryonic", "Too little", "Lessened", "Narrowed"]

### 8. **Misused or Misdirected**

> 'Misfiring, misuse, or misdirection implies a faulty start, bad timing, or something that is not used appropriately. … Try other forms of the prefix mis-.' (Greer 2002)

[Distortion or deviation from the card's true nature.]

**Summary**: Reversals as a kind of distortion or deviation from the card's "true" nature. Each reversed card represents a point where the querent's application of that energy has gone awry. This aligns with an ontology that sees the tarot archetypes as having true, essential natures that can be misapplied through human error or misunderstanding. Reversals represent a departure from the card's authentic expression. Procedurally, interpreting a reversal as "misused" or "misdirected" involves identifying how the card's upright energy is being misapplied in the querent's situation, and suggesting corrective actions.

Ontographically, this frames the tarot reading as a landscape of potential misalignments. The spread becomes a map of areas needing correction or realignment.

It also resonates with the idea of the "shadow" in Jungian psychology, where unintegrated aspects of the psyche can manifest in distorted or problematic ways. Reversals could represent the querent's shadow energies needing integration.

In an object-oriented `Card` class model, this could be represented through a `misuse_type` attribute, perhaps an enum or string, indicating the specific way the card's energy is being misapplied.

In a procedural model, this could involve functions like `diagnose_misuse()` and `suggest_realignment()` that analyse the querent's situation and propose ways to redirect the card's energy. Applying this technique would involve first calling `diagnose_misuse()` to identify the specific way the card's energy is being misapplied, then passing that to `suggest_realignment()` to generate advice for the querent.

The interpretation could draw on a knowledge base of common misuses and misdirections associated with each card, and corresponding corrective actions. For example, the reversed Chariot might suggest the querent is misusing their willpower to control others rather than master themselves.

Over a series of readings, the program could track patterns in the querent's misuses, offering insights into recurring shadow tendencies or areas for growth. It could celebrate when previously misused energies show up in upright positions, reflecting successful integration (lol what, imagining a confetti animation).

Modelling this in the data structures and algorithms of the tarot program would position Querent.py as a kind of "wise friend" or mentor, helping the querent recognise where they've gone off track and gently guiding them back to the authentic expression of each card's highest potential. (Bit paternalistic?)

["Misused", "Misdirected", "Misplaced", "Mistrust", "Mishap", "Mistaken", "Miss", "Instability", "Irresponsible", "Problematic", "Inappropriate"]

### 9. **"Re-" Words: Retried, Retracted, Reviewed, Reconsidered**

> 'Reversals immediate suggest other "re-" words such as those above. The prefix "re-" denotes backward motion, withdrawal, opposition, negation, or to do again.' (Greer 2002)

[Reflection, correction, and reevaluation.]

**Summary**: Reversals as markers of change, correction, or opposition to the card's initial state. Each reversed card represents a point of reflection or course correction in relation to the upright meaning. Reversals mark moments of opposition and negation spurring reevaluation. Reversals prompt the querent to revisit their assumptions, reconsider their actions, and potentially change course. Each reversal becomes an invitation to look again with fresh eyes, charting a new course if needed.

(It's kind of processual?) Ontographically, this frames the tarot reading as a space of potential revision and reconsideration. This aligns with an ontology of change and process, where the meanings of the cards are not fixed but subject to ongoing adjustment.

In an object-oriented `Card` class model, this could be represented through a `reversed_action` attribute, perhaps an enum or string, indicating the specific "re-" action associated with the reversal.

Procedurally, interpreting a reversal as a "re-" action involves identifying the initial upright meaning, and then applying the specific "re-" operation to generate the reversed interpretation. In a procedural model, this could involve functions like `apply_reversal()` that take the upright meaning and the "re-" action and return the modified interpretation.

Applying this technique would involve setting the reversed_action attribute of reversed cards, then calling `apply_reversal()` with the card's `upright_meaning` and `reversed_action` to generate the interpretation. The interpretation could suggest reflections or actions for the querent to take in light of the "re-" action. For example, a "reconsidered" reversal might prompt the querent to question their assumptions about the upright meaning.

Procedurally, this technique lends itself to an iterative, dialogic model of tarot reading, where the interpretation of a card is not a one-time event but an ongoing process of reflection and revision. Each reversal becomes an invitation to look again with fresh eyes, charting a new course if needed.

["Retreated", "Reconsidered", "Reviewed", "Retracted", "Retrograde", "Reverse direction", "Rectified", "Relieved", "Relaxed", "Returned", "Renewed", "Remedied", "Rectified", "Relieved", "Redeemed", "Corrected", "Countered"]

### 10. **Unconventional, Shamanic, Magical, Humorous**

> 'If an upright card depicts conventional siwdom, then the reversal illustrates unconventional wisdom. It quests all the assumptions indicated by the upright meaning. It is not straight, but crooked and crazy. Each card has a place that you can "see through and into." you have to look under the mask of what "seems to be." Thus there could be a trickster aspect to a reversed card. Perhaps a sense of humour is required; you are being instructed not to take the situation too seriously. … The shamanic or magical view, in particular, asks you to enter the card and journey to an Alice-in-Wonderland realm in order to bring back a vital message or understanding.' (Greer 2002)

[Subversion, unconventional wisdom, and Trickster energy.]

**Summary**: Reversed cards as a subversion or inversion of conventional wisdom, revealing hidden or unconventional truths. Reversals serve as indicators that we need to question our assumptions and look beyond the obvious. This resonates with the Jungian concept of the Trickster archetype, a boundary-crossing figure who subverts norms and reveals unexpected insights. Reversed cards may embody this Trickster energy, playfully challenging our preconceptions. Procedurally, interpreting a reversal through this lens involves a kind of perspectival shift or cognitive reframing. The querent is invited to step outside their conventional viewpoint and entertain a radically different, even humorous or absurd, perspective.

Ontographically, this frames the tarot reading as a liminal space where conventional meanings can be overturned, and hidden wisdom can emerge. This aligns with an ontology that sees reality as multi-layered, with surface appearances masking deeper, often paradoxical truths.

In an object-oriented `Card` class model, this could be represented through a `reversed_perspective` attribute, perhaps a string or array, holding the unconventional or trickster-like meanings associated with the card's reversal.

In a procedural model, this could involve functions like `conventional_meaning()` and `unconventional_meaning()` that return different interpretations based on the card's reversal status. Applying this technique would involve first setting the `reversed_perspective` attribute with an appropriate unconventional meaning, then calling the `unconventional_meaning()` function for reversed cards.

The interpretation might encourage the querent to question their assumptions, look for humor in the situation, or embrace a "crooked" path. Procedurally, this technique lends itself to a more open-ended, exploratory style of tarot reading, where unexpected insights are welcomed and conventional meanings are held lightly. 

["Humorous", "Trickster", "Coyote", "Joke", "Topsy-turvy", "See through", "Unconventional", "Contrary", "Subverted", "Iconoclastic", "Crooked", "Baffled", "Twisted", "New Perspective"]

## Prototyping

### Key Considerations:

1. Presenting multiple reversal interpretations to the querent can provide rich insights but risks cognitive overload. An iterative, dialogic approach can help manage this complexity (are there other ways?).
2. Combining complementary techniques into more abstract transformations can strike a balance between interpretive richness and coherence. This requires careful analysis of the techniques' underlying principles.
3. The overall goal is to scaffold the querent's own meaning-making process, eliciting their reflections and associations to populate an evolving personal dictionary. The data model should be designed to support this incremental growth.
4. Refactoring the `Card` class and EAV model to accommodate multiple reversal techniques is best approached iteratively, allowing for testing and reflection at each stage.

### Potential approach

1. Analyse the 10 techniques to identify underlying principles and complementarities. For example, "Blocked/Resisted" and "Delayed/Difficult" both involve a hindrance to the card's energy, while "Inner/Unconscious" and "Projected" both deal with psychological dimensions.
2. Based on this analysis, develop a set of more abstract reversal transformations that combine related techniques.

    - "Hindrance" (combining Blocked/Resisted, Delayed/Difficult)
    - "Shadow" (combining Inner/Unconscious, Projected)
    - "Reversal" (combining No/Not, Lacking)
    - "Excess" (Excessive/Over-compensating)
    - "Misdirection" (Misused/Misdirected)
    - "Reconsideration" (Re- words)
    - "Subversion" (Unconventional/Shamanic)

3. Refactor the `Card` class to include these abstract transformations as optional attributes, each pointing to a dictionary of the relevant techniques and their generated interpretations.

```
class Card:
    def __init__(self, name, upright_meaning):
        self.name = name
        self.upright_meaning = upright_meaning
        self.reversed = False
        self.hindrance = None
        self.shadow = None
        self.reversal = None
        # ... other transformations

    def generate_reversal(self, transformation, technique, querent_input):
        # Generate reversal interpretation based on technique and querent input
        # Store in the relevant transformation dictionary
        self.transformation[technique] = interpretation
```

4. Develop an interactive dialogue system that presents the querent with the abstract transformations relevant to their drawn card(s), based on some initial criteria (e.g., the querent's situation, the spread position meaning, etc.).
5. For each selected transformation, guide the querent through a series of prompts and questions to elicit their reflections, associations, and interpretations. Use this input to generate personalized reversal interpretations using the underlying techniques.
6. Present the querent with the generated interpretations, highlighting complementarities and tensions between the different techniques. Encourage further reflection and refinement.
7. Store the querent's finalized interpretations, associations, and reflections in their personal dictionary, linked to the relevant `Card` and transformation. Over time, this dictionary becomes a rich resource for personalized readings.
8. Iterate on the `Card` class and EAV model design based on insights from implementing and testing this dialogue system. Refine the abstract transformations and data structures as needed to better support the querent's meaning-making process.

### Potential challenges

- Balancing structure and openness in the dialogue system to guide the querent's reflections while allowing for emergent insights
- Managing the complexity of multiple transformations and techniques in the user interface and data model
- Developing natural language processing capabilities to generate meaningful interpretations from the querent's input.
- Ensuring the evolving personal dictionary remains coherent and navigable as it grows over time
- Designing for the edge cases of contradictory or incompatible interpretations across techniques

### Suggested procedures

#### 1. "Obstacles and Challenges" (Blocked/Resisted + Delayed/Difficult)

This transformation captures the essence of resistance, delays, and difficulties. It represents situations where the card's energy is hindered or obstructed.

#### 2. "Shadow" (Projected + Inner/Unconscious/Private)

This transformation focuses on the internal, hidden, or psychological dimensions of the card's energy. It represents aspects of the self that are projected, unconscious, or private.

#### 3. "Transformation and Change" (Breaking Through/Overturning + "Re-" Words)

This transformation highlights moments of change, reflection, and reevaluation. It represents pivotal choice points and the need to reconsider or correct one's path.

#### 4. "Imbalance and Misapplication" (Misused/Misdirected + Excessive/Over/Undercompensating)

This transformation addresses the misapplication or imbalance of the card's energy. It represents situations where the card's energy is either excessive, deficient, or misdirected.

#### 5. "Binary Negation" ("No/Not/Lacking")

This transformation serves as a baseline or entry point, representing the straightforward negation or absence of the card's core qualities.

#### 6. "Subversion" (Unconventional/Shamanic)

This transformation captures the unconventional, subversive, and humorous aspects of the card's energy. It represents the Trickster archetype and the need to question assumptions.