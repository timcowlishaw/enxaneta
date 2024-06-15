# Working Notes 1: Modelling Tarot Reversals

In basic terms, I'm currently grappling with how to model card reversals in this weird little shonky tarot-reading prototype Python programme I've been working on. With the Tarot de Marseille as my main go-to, for now, I _think_ I only want reversals to apply to cards in the Major Arcana, based on it being difficult to discern the orientation of the "pips" of the Minor Arcana (?), but this is up for debate.

I'm leaning towards a `Card` object class, as something that supports some of my other plans, and will (I think?) enable tracking and analysis (e.g. percentage of reversed cards in a given spread, different cards' orientations over time). That said, I'm keen to avoid accidentally painting myself into a corner, and want to make sure I haven't overlooked any obvious issues or drawbacks.

Keen to encode Jodorowsky's philosophy into the procedural rhetoric of the model, defaulting to open-ended questions and prompts that encourage self-reflection when a reversal appears, rather than definitive statements. Guide the querent to find their own meaning.

## "Yes, but what _is_ a reversal?"


> 'In general, it helps to think of reversed cards as "red flagged," indicating that you should pay extra attention to them. They signal that something is not operating as usual. Upright cards tend to be conscious, outer, automatic, in process, and available. Reversed cards often indicate choice points, where you must be attentive. They may require conscientious, willful handling if you are to take full advantage of the energies and opportunities. It is like knowing that a car has a tendency to pull to the right and so you have to keep alert and make adjustments for it. Or they are places to stop struggling, relax, and let go of all expectations.' (Greer 2002: 25)

In tangible, material terms, reversed cards in a reading are a result of blind shuffling. Rather than just a upright/reversed binary, reversals gesture to a spectrum of interpretive meanings for each card. A reversal can indicate the energy of the card is blocked, turned inwards, early or late in its appearance, or manifesting in a more challenging or "shadow" form.

I'm interested in modelling reversals in a way that is less about opposition or negativity, and more about a card's _latency_, or hidden properties (blockages, delays, etc.).

Reading with reversals also requires considering the _relationship_ between reversed and upright cards. If lots of cards are upright, the few reversals stand out more, and vice versa. 

Ways to see through to "the other side", going beyond the limits of the known? A realm of potentials and underlying causes. All a bit subjunctive? A reminder that situations and energies are not fixed or static, but constantly shifting.

A way of adding nuance (though: cf. Kieran Healy, "[Fuck Nuance](https://kieranhealy.org/files/papers/fuck-nuance.pdf)"), destablising and swerving away from the fixed, immutable dictionary approach to tarot interpretation.

From an OOO perspective, the reversal activates a _different set of capacities_ within the card-object. The reversed position reconfigures the card's internal composition and its relations to the other cards in the spread, opening up new lines of interpretation and insight. From this standpoint, the choice to read reversals or not is less about technical proficiency or interpretive sophistication, and more about the reader's orientation to the cards as meaning-making objects. Reading reversals could be seen as a way of _attending to the hidden depths and alternative potentials lurking within each card_.

If the upright card represents one set of attributes, a reversal is one of multiple possible lenses transforming that set. The interpretive challenge is in figuring out which transformations should be applied, through querent input and contextual analysis.

Mary Greer presents a longer list of possible reading techniques (10 of which I work with below), but an even shorter heuristic comes in James Ricklef's "Five Ds": 1. _Delay_ of the original effect; 2. _Diminuation_ of the original effect; 3. _Direct opposite_ of the original meaning; 4. _Dark side_ of the original meaning; 5. _Direction change_.

## 12 ways to read reversals (Greer 2002); of which the following 10 are relevant to us:

1. **Blocked, Resisted**: Obstacles, hindrances, and resistance to the card's energy. ("Blocked", "Stuck", "Stymied", "Thwarted", "Struggled with", "Denied", "Avoided", "Defied", "Resisted", "Repressed", "Refused", "Rejected")

2. **Projected**: Psychological mirroring, reflecting denied or disowned aspects of the self: qualities we may see in others but fail to recognise in ourselves. The reversal acts as a kind of flip, _turning the card's energy outward_ rather than inward. 

3. **Delayed, Difficult, Unavailable**: Temporal challenges, delays, and difficulties in manifesting the card's energy. Each card contains latent potentials that may be delayed, made difficult, or rendered temporarily unavailable by a reversal. The reversal doesn't negate the card's core meaning, but rather modifies the ease and timeline of its manifestation. Temporary challenges, rather than permanent, immutable obstacles. ("Delayed", "Hestitated", "Held back", "Set back", "Made difficult", "Rough road", "Indecisive", "Distracted", "Obstructed", "Hindered", "Suspended", "Inhibited", "Turned away from")

4. **Inner, Unconscious, Private**: Internal, hidden, or unconscious aspects of the card's energy. This technique maps the tarot system onto a model of the psyche, with upright cards representing conscious phenomena and reversals representing the querent's unconscious or internal state. ("Inner", "Inward", "Unconscious", "Internal", "Personal", "Private", "Deep", "Secret", "Covert", "Unexpressed", "Indirect", "Underground", "Underlying", "Concealed", "Unseen", "Beneath", "Below")

5. **Breaking Through, Overturning, Refusing, Changing Direction**: Transformative thresholds, pivotal choice points, and active change. This frames the reading as a space of potential transformation, a landscape of thresholds and pivotal moments. Reversals mark points of instability where new possibilities can emerge through the querent's choices. The reversed card is an assertion of agency, an invitation to overturn determinism. ("Overturned", "Overthrown", "Overcome", "Broken through", "Put down", "Changed", "Adjusted", "Toppled", "Out from under", "Falling away", "Unseated", "Breached", "Loosened", "Freed", "Released")

6. **No or Not (X); Lacking**: Binary negation or absence of the card's core qualities. The reversal flips the card's polarity. A simple "ground level" of reversal, a _first approximation_ of the card's inverted meaning that sets the stage for deeper, more individualised interpretations. ("No", "Not", "Negated", "Inverse of", "Lacking", "Absent", "Without", "Ended", "End of", "Discontinued")

7. **Excessive, Over- or Undercompensating**: Spectrum of intensity, over- or under-expression of the card's energy. Frames the reading as a landscape of energetic intensities, or a map of imbalances and compensations, with each card manifesting its archetypal meaning to a greater or lesser degree. Modelling a dynamic system (the psyche?) seeking equilibrum. ("Too much", "Too strong", "Overwhelmed", "Overly", "Excessive", "Exaggerated", "Intensified", "Overindulged",  "Ungrounded", "Out of control", "Tentative", "Toned down", "Softened", "Embryonic", "Too little", "Lessened", "Narrowed")

8. **Misused or Misdirected**: Distortion or deviation from the card's true nature. Each reversed card represents a point where the querent's application of that energy has gone awry. The spread becomes a landscape of potential misalignments. Interpreting a reversal as "misused" or "misdirected" involves identifying how the card's upright energy is being misapplied in the querent's situation, and suggesting corrective actions. ("Misused", "Misdirected", "Misplaced", "Mistrust", "Mishap", "Mistaken", "Miss", "Instability", "Irresponsible", "Problematic", "Inappropriate")

9. **"Re-" Words: Retried, Retracted, Reviewed, Reconsidered**: Reflection, correction, and/or reevaluation. Reversals mark moments of opposition and negation, spurring reevaluation. The reading becomes a space of revision, subject to ongoing adjustment. Each reversed card becomes an invitation to look again with fresh eyes, charting a new course if needed. ("Retreated", "Reconsidered", "Reviewed", "Retracted", "Retrograde", "Reverse direction", "Rectified", "Relieved", "Relaxed", "Returned", "Renewed", "Remedied", "Rectified", "Relieved", "Redeemed", "Corrected", "Countered")

10. **Unconventional, Shamanic, Magical, Humorous**: Subversion, unconventional wisdom, and Trickster energy. The reversed cards invert conventional wisdom, revealing hidden or oblique truths. Reversals serve as indicators that we need to question our assumptions and look beyond the obvious. Reversed cards may embody a boundary-crossing, norm-subverting Trickster energy, playfully challenging or reframing our preconceptions. The reading becomes a liminal space where conventional meanings can be overturned, and hidden wisdom can emerge. The querent is invited to step outside their conventional viewpoint and entertain a radically different, even humorous or absurd, perspective. ("Humorous", "Trickster", "Coyote", "Joke", "Topsy-turvy", "See through", "Unconventional", "Contrary", "Subverted", "Iconoclastic", "Crooked", "Baffled", "Twisted", "New Perspective")

## Prototyping

### Key assumptions

1. Presenting multiple reversal interpretations to the querent can elicit more meaningful, personalised insights, but also risks cognitive overload. An iterative, dialogic approach can help manage this complexity (are there other ways?).
2. Combining complementary techniques (from Greer 2002) into more abstract transformations can strike a balance between interpretive richness and coherence. This requires careful analysis of the techniques' underlying principles.
3. The overall goal is to scaffold the querent's own meaning-making process, eliciting their reflections and associations to populate an evolving personal dictionary. The data model should be designed to support this incremental growth.
4. Refactoring the `Card` class and data model to accommodate multiple reversal techniques is best approached iteratively, allowing for testing and reflection at each stage.

### Potential approach

1. [x] Analyse Greer's 10 techniques to identify underlying principles and complementarities. Based on this analysis, develop a set of more abstract reversal transformations that combine related techniques.
2. Refactor the `Card` class to include these abstract transformations as optional attributes, each pointing to a dictionary of the relevant techniques and their generated interpretations.
3. Develop an interactive dialogue system that presents the querent with the abstract transformations relevant to their drawn card(s), based on some initial criteria (e.g., the querent's situation, the spread position meaning, etc.).
4. For each selected transformation, guide the querent through a series of prompts and questions to elicit their reflections, associations, and interpretations. Use this input to generate personalised reversal interpretations using the underlying techniques.
5. Present the querent with the generated interpretations, highlighting complementarities and tensions between the different techniques. Encourage further reflection and refinement.
6. Store the querent's finalised interpretations, associations, and reflections in their personal dictionary, linked to the relevant `Card` and transformation. Over time, this dictionary becomes a rich resource for personalised readings.
7. Iterate on the `Card` class and data model design based on insights from implementing and testing this dialogue system. Refine the abstract transformations and data structures as needed to better support the querent's meaning-making process.

### Challenges

- Balancing structure and openness to guide the querent's reflections while allowing for emergent insights
- Managing the complexity of multiple transformations and techniques in the user interface and data model
- Developing natural language processing capabilities to generate meaningful interpretations from the querent's input
- Ensuring the evolving personal dictionary remains coherent and navigable over time
- Designing for the edge cases of contradictory or incompatible interpretations across techniques

## Prototyping in-progress

```python
class Card:
    def __init__(self, name, upright_meaning):
        self.name = name
        self.upright_meaning = upright_meaning
        self.reversed = False
        self.negation = None # Do we need a seperate negation attribute, or could this be inferred from the reversed Boolean, if no other reversal/transformation attributes are active?
        self.obstruction = None
        self.imbalance = None
        self.shadow = None
        self.transformation = None
        self.subversion = None

    def generate_reversal(self, transformation, technique, querent_input)
        # Generate reversal interpretation based on technique and querent input
        # Store in the relevant transformation dictionary
        self.transformation[technique] = interpretation
```

### Transformations

I think we're going to try modelling 6x broad transformations, bundling related techniques identified by Mary Greer under headings of "negation" (the "ground level" or baseline transformation), "obstruction", "imbalance", "shadow", "transformation", and "subversion" (a bit of a wildcard).

#### 1. "Negation" ("No/Not/Lacking")

Negation suggests a binary switch or toggle, where the reversed meaning is a direct inversion or absence of the upright. Modeling this could involve a boolean `reversed` attribute on the `Card` class, which, when `True`, negates or nullifies the upright meaning.

The program would present reversed cards as negations of their upright meanings, suggesting a clear inversion or lack. Querent interactions would involve grappling with the implications of this absence or opposition, considering what's missing or contrary to their expectations.

e.g. If the upright Empress represents abundance and nurturing, a "negated" reversal would be interpreted as "No abundance" or "Lacking nurturing." The querent would be prompted to reflect on areas of scarcity or deficiency in their life related to the Empress's themes.

e.g. If the upright Chariot represents forward momentum and control, a "Negation" reversal might suggest "Lacking direction" or "No momentum". The program could prompt the querent to reflect on areas where they feel directionless or powerless.[^1]

Ontographically, this technique maps the tarot's symbolic world onto a binary space of presence and absence.[^2]

```python
class Card:
    def __init__(self, name, upright_meaning):
        self.name = name
        self.upright_meaning = upright_meaning
        self.reversed = False

    def meaning(self):
        if self.reversed:
            # Negate the meaning (the keywords?) by prepending (e.g.) "No" or "Lacking"
            return f"No {self.upright_meaning}" or f"Lacking {self.upright_meaning}"
        else:
            return self.upright_meaning
```

Using a Boolean aligns with the ontological framing of reversals as a binary switch, toggling between the presence and absence of a card's core qualities. It's a straightforward way to represent the negation technique within the object-oriented structure of the `Card` class.

Reason to model reversals-as-negations with an attribute rather than a function, at least initially, is because we want querent-elicted interpretations and associations to get "attached" to the card; latent but remembered, available for future retrieval.

If this a "ground level" reversal, a _first approximation_ of the card's inverted meaning, as a placeholder and prelude to greater semantic (?) resolution or fidelity to the situation at-hand, I guess we're looking at a `negate()` function, appending "no", "not", "non-", "un-" or "lacking" to the `upright_meaning` or default keyword strings, which then get shown to the querent as a dialogue prompt? A practical entry point, this is the "baseline" interpretive procedure/operation from which the other transformations depart.

#### 2. "Obstruction" (Blocked/Resisted + Delayed/Difficult)

Obstruction implies a hindrance or barrier to the (easy, timely) manifestation/expression of the upright meaning. The reversed card's energy is present but impeded. Modeling this will probably involve including an `obstruction` attribute on the `Card` class, which could be an enum or a string indicating the type of obstruction (e.g., "DELAYED", "THWARTED", "GATED", "UNAVAILABLE"[^3]).

The `meaning()` method could be modified to return different interpretations based on the obstruction attribute's value, encapsulating the reversal logic within the method? When interpreting a reversed card, the program would first check the `obstruction` attribute to determine the type of obstruction. Based on the obstruction type, the program would apply the corresponding operation to the card's base, upright `meaning` (or `archetype`?).

The program would frame reversed cards as temporary challenges rather than permanent, immutable obstacles. Querent interactions would involve identifying and engaging with these barriers. The program should emphasise the querent's agency and ability to overcome blockages and delays. This could be based on predefined mappings between obstruction types and suggested actions, presented as prompts or questions.

e.g. An obstructed Chariot might be interpreted as "Progress blocked" or "Victory delayed." The querent would be guided to consider what internal or external factors are impeding their forward momentum, and how they might work through these challenges.

```python
card = Card("The Chariot", "Willpower, determination, victory")
card.set_reversal(True)
card.set_obstruction(ObstructionType.BLOCKED, "Feeling stuck, lack of progress")

print(card.get_meaning())
# Output: Blocked: Feeling stuck, lack of progress
```

The program could also track the presence and frequency of obstructions across a querent's multiple readings, identifying recurring patterns of blockage or delay and offer insights or recommendations based on these patterns.

#### 3. "Imbalance" (Misused/Misdirected + Excessive/Over/Undercompensating)

Imbalance points to a distortion or misapplication of the card's upright energy. The reversal isn't a negation but a deviation from the ideal expression, suggesting a need for recalibration. Modeling this could use a `imbalance` attribute.

Could define an `imbalance` enum to represent the different types of imbalance (e.g., "MISUSED", "MISDIRECTED", "EXCESSIVE", "DEFICIENT", "NARROW", "UNSTABLE", "INAPPROPRIATE"), providing a structured way to categorise and interpret the nature of the imbalance in reversed cards.

Could include a `diagnose_imbalance()` (`discern_imbalance`?) function that analyses the querent's situation and the card's upright meaning to determine the specific type of imbalance present in a reversed card. This could involve a dialogic interaction with the querent, or pattern matching against common misuses or misdirections associated with each card.

```python
def diagnose_imbalance(card, querent_situation):
    # Review querent_situation and card.upright_meaning
    # to determine the type of imbalance
    # Return an Imbalance enum value
    pass
```

```python
def interpret_imbalance(card):
    if card.imbalance == Imbalance.MISUSED:
        return f"{card.name}'s energy of {card.upright_meaning} may be misused or misapplied."
    elif card.imbalance == Imbalance.EXCESSIVE:
        return f"An excessive or overcompensating expression of {card.name}'s {card.upright_meaning}."
    # ... handle other Imbalance types
```

Ontographically, this transformation frames the tarot reading as a landscape of energetic intensities and/or potential misalignments. The spread becomes a map of imbalances and compensations, pointing to areas of excessive, deficient, or misapplied expression, needing correction or realignment. Each reversed card represents a point where the application that energy has gone awry.

The program will present reversed cards as imbalanced expressions of their upright qualities, inviting the querent to consider where and what they may be over- or under-doing.

e.g. An excessively imbalanced Hermit might be interpreted as "Excessive isolation." The querent would be prompted to reflect on where they may be taking the Hermit's qualities of solitude and introspection to an unhealthy extreme.

#### 4. "Shadow" (Projected + Inner/Unconscious/Private)

Shadow suggests the reversal turns the card's energy inward, pointing to unconscious or shadow aspects of the querent's psyche. It sets up a distinction between the external and the internal, the conscious and the unconscious. Modeling this could use a `shadow` attribute.

The program would frame reversed cards as reflections of the querent's inner state or unacknowledged projections. Interactions would involve introspection and shadow work.

```python
def interiorise(self, card_meaning):
    return f"In your inner world, {card_meaning.lower()}" # "Lower"? No idea what's going on here
```

In a procedural model, this could involve a `project_attributes(querent)` method on the `Card` class that compares the `projected_attributes` to the `querent` object's own attributes (!!!), looking for matches or discrepancies. This method could return a interpretation string highlighting any projections.

e.g. A shadow reversal of the Lovers might be interpreted as "Unconsciously projecting relationship ideals" or "Inner conflicts around partnership." The querent would be guided to examine their own unacknowledged desires and fears around love and intimacy.

**Alternatively** (my preference): Instead of representing the querent's personal shadow, reversed cards could point to collective or archetypal shadow energies associated with the card. This frames reversals as portals into the universal unconscious, rather than the querent's private psyche. In the data model, this could be represented through a `shadow_archetype` attribute on the `Card` class, holding a symbolic description of the card's reversed meaning, e.g., "Repressed creativity", "Unacknowledged grief", "Denied power".[^4]

Interpreting a reversal would involve looking up the card's shadow_archetype and reflecting on how that archetypal energy might be manifesting in the user's situation, without requiring direct psychological analysis. Reversed cards could be treated as invitations for the querent to dialogue with the shadow archetype.

This positions the reading as a dialogue between the user's conscious situation and the deeper archetypal energies in play. The spread becomes a map of the interplay between light and shadow.

**Or**: Even more broadly, this transformation could access "hidden" or "latent" dimensions of the cards upright meaning? We'd need to give some thought to what this might look like in practice; perhaps using enums (e.g. "DEEP", "CONCEALED", "UNEXPRESSED", "INDIRECT", "UNDERGROUND").

#### 5. "Transformation" (Breaking Through/Overturning + "Re-" Words)

"Transformation" frames reversals as catalysts for change and/or reorientation, pivots or turning points where old patterns can be overturned. The querent might be getting out from under, breaking free of, rejecting, refusing, or turning away from the energy or condition depicted. It could also designate the end or passing of a situation, a loosening, or change in direction. The "transformation" operation (?) emphasises process over state, framing the upright and reversed meanings as part of an ongoing evolution. A reversed card becomes a fork in the path, inviting the querent to overturn old patterns or correct course.

The technique frames reversals as markers of instability and potential transformation, aligning with an ontology of becoming and emergence. The meanings of the cards are fluid and dynamic. How do we model this fluidity in the data structure? Should we allow for multiple, context-dependent interpretations of each reversal, and if so, how do we manage the resulting complexity?

This could involve adding a `transformation` attribute to the `Card` class, which could be an enum or string indicating the specific type of transformative energy associated with the reversal (e.g., "TOPPLING", "BREAKING_THROUGH", "LOOSENING", "RETRACTING", "RECONSIDERING", "REDEEMING"[^5]). 

**Alternatively**: We could use a boolean `catalyst` attribute (or similar) to signal whether the reversal represents a transformative catalyst, and then determine the specific transformation type procedurally based on the card's other attributes and the querent's situation. (Seems like a bit of a faff.)

```python
    def apply_reversal(self, relationship):
        if self.catalyst:
            if relationship == "stuck":
                return f"Breaking free from limitation: {self.upright_meaning}"
            elif relationship == "resisting":
                return f"Overturning resistance: {self.upright_meaning}"
            # Add other relationship mappings as needed
        else:
            return f"Reconsidering: {self.upright_meaning}"
```

(I like this. Three pipes, for example, with a default. How to make these pipes sufficiently chunky?)

**Or**: Implement an `assess_relationship()` function that takes the querent's situation (perhaps as a string or a more structured object) and the card's upright meaning, and returns a description of the querent's current relationship to that energy (e.g., "stuck", "resisting", "outgrowing"). Then create a `propose_reversal()` function that takes the querent's current relationship to the upright meaning (from `assess_relationship()`) and generates a transformative reversal interpretation.

Procedurally, interpreting a reversal as "breaking through" or "changing direction" involves identifying the querent's current relationship to the upright meaning, and then signaling a potential point of departure or transformation. Ontographically, this frames the tarot reading as a space of potential revision and reconsideration. This aligns with an ontology of change and process, where the meanings of the cards are not fixed but subject to ongoing adjustment.

```python
querent_context = "Feeling stuck in a rut"
transformed_card = card.transformation(querent_context)
print(transformed_card.reversed_meaning)
```

How to structure the elicitation of `querent_context`? The program could elicit `querent_context` before the reading by asking a series of questions or by providing a text input field, as a "focus" question. This could be done at the beginning of the reading or as part of the reading process.

```python
    def assess_relationship(self, querent_input):
        # Placeholder for assessing the querent's relationship to the upright meaning
        # This could involve NLP techniques or predefined mappings
        return "stuck"  # Example output

    def propose_reversal(self, relationship):
        if relationship == "stuck":
            return TransformationType.BREAKING_THROUGH
        elif relationship == "resisting":
            return TransformationType.OVERTURNING
        # Add other mappings as needed
```

The program would present reversed cards as invitations or opportunities for growth and change. Querent interactions would focus on identifying and engaging with these transformative openings. The program should facilitate this active engagement, providing tools and prompts that empower the querent to explore and enact transformative changes.

e.g. A "reconsidering" reversal of the Tower might be interpreted as "Reconsidering upheaval" or "Revelation reconsidered." The querent would be prompted to reflect on the value (or not) of Tower's disruptive energy at this point in time.[^6]

```python
tower_card = Card("The Tower", "Upheaval", "Revelation", "Awakening") # How will the card  handle keywords?
tower_card.set_transformation_type("reconsidering")
querent_state = "feeling trapped"
if tower_card.assess_relationship(querent_state):
    reversed_interpretation = tower_card.propose_reversal()
    print(reversed_interpretation) # Example output: "Reconsidering upheaval: The Tower suggests reconsidering sudden change.
```

Philosophically, this operation resonates with ideas of self-creation, framing the querent as an agent actively shaping their path, not just passively receiving the cards' meanings. The "transformation" reversal is a "clinamen", an invitation to overturn determinism.

- How do we encode the specific actions or reflections associated with each transformation type? Should these be predefined or generated dynamically (procedurally?) based on the querent's input?
- How do we guide the querent through the process of identifying their relationship to the upright meaning and proposed transformation? Should we use a decision tree, an iterative dialogue, or another method to scaffold this interaction?

#### 6. "Subversion" (Unconventional/Shamanic)

Subversion positions reversals as challenges to conventional wisdom, revealing unexpected, oblique, or even absurd perspectives. It emphasises the contextual fluidity of interpretation, and the value of unorthodox insight.

Operationalising the trickster archetype and/or shamanic wisdom is no mean feat. The program needs to generate subversive interpretations that are still meaningful and relevant to the querent's situation. This involves balancing randomness with coherence.

We could implement a `subversion` attribute on the `Card` class to store unconventional or trickster-like meanings associated with reversals. This could be a string, array, or even a nested object with multiple subversive interpretations.

We might want a function or method to generate subversive reversal interpretations based on the upright meaning. This could involve:

- Identifying and inverting key concepts or assumptions in the upright meaning
- Applying humour, irony, or absurdity to the upright meaning[^7]
- Drawing from a predefined set of unconventional or trickster-like archetypes or themes

We want a function that takes the upright meaning as an input, and returns a subverted or ironised version. Juxtaposition, exaggeration, reframing, alternative viewpoints?

Are we looking at a predefined dictionary of subversive interpretations? Not entirely sold on these examples, but:

```python
def subvert_meaning(card, upright_meaning, querent_input):
    subversions = {
        "The Fool": [
            "The wisdom of folly: embracing the unknown with reckless abandon.",
            "The holy fool: finding enlightenment in the absurd and the unexpected."
        ]
    }
```

The program needs to frame reversed cards as invitations to question assumptions and entertain alternative viewpoints. Querent interactions should support playful, lateral, or oblique engagement with the cards' meanings. The querent could be invited to question their assumptions about the situation or the card's upright meaning ("What else might be going on here?"); look for humour/irony, opportunity, or unexpected lessons in challenging circumstances; or consider how a trickster might approach or _reframe_ the issue at hand.

```python
def generate_subversive_prompts(card):
    prompts = [
        f"How might a trickster see the humor or opportunity in {card.subversive_meaning()}?",
        f"What assumptions are being challenged by {card.subversive_meaning()}?",
        f"Consider how {card.subversive_meaning()} might offer a new perspective on your current situation."
    ]
    return prompts
```

## Desmuntar

[^1]: (J) In this example, "Lacking control" might not be as clean as "Out of control" or "Uncontrolled". We might want to consider a more sophisticated negation strategy, taking into account the specific meaning of each card.
[^2]: (J) However, this binary ontology does risk reducing the tarot's symbolic richness to a series of on/off switches, losing sight of more subtle shades of significance. As Greer cautions (and Jodorowsky echoes), a purely mechanical negation risks generating interpretations that are overly machinic or pessimistic. The program may need to incorporate additional heuristics to maintain a balanced perspective.
[^3]: (J) Deliberately ridiculous examples; need to figure out a proper enum grammar.
[^4]: (J) This is better, I think. Less ethically dubious, in terms of accidentally harvesting loads of sensitive user data. A way of honouring the querent's autonomy, even if/as they are just one object among many (lol).
[^5]: (J) I think it makes sense to format these as verbs, foregrounding the processual nature of the operation.
[^6]: (J) A little bit tenuous, but let's see.
[^7]: (J) Ah yes, operationalising humour, what could possibly go wrong? ("What _is_ irony?" etc.)