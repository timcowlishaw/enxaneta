# Working Notes 5: Speculating on the "Humus-Querent-ELIZA Stack"

So, let's see: Tim's working on [Humus](https://github.com/timcowlishaw/humus), a composting database in Rust.

> 'This is a small experiment in deliberate data decay. a simple (at present) in memory [entity-attribute-value database](documentation\working_notes\02_eav-data-model.md) that slowly forgets the things that you don't revisit.'

This database structure challenges the dominant "accumulation" model of typical digital systems. It aligns with permacomputing principles by questioning resource use and data permanence. Tim's use of Rust is a bit of an Oulipic constraint, but also suggests a focus on performance and memory safety.

Humus is a permacomputing-inspired "composting database" rendered in Rust, Querent is a Python tarot-reading programme inspired by the work of Ian Bogost and Alejandro Jodorowsky, and ELIZA is the 1960s chatbot developed by Joseph Weizenbaum.

## The Stack

1. User interacts with an ELIZA-like interface, which prompts for input and guides the tarot reading process.[^1]
2. Querent.py handles the tarot-specific logic, drawing cards, and generating initial interpretations.
3. These interpretations are stored in and retrieved from Humus, which allows for the accumulation and gradual decay of meanings over time.[^2]
4. The ELIZA interface then presents these interpretations back to the user, encouraging further reflection and input.[^3]
5. New insights and interpretations from the user are fed back into the system, stored in Humus, and influence future readings.

## Further notes

_Creating_ compression artifacts, as a spur to defamiliarisation and recontextualisation.

The Querent is the person seeking information or insight from a tarot reading. The term comes from the Latin "quærēns", meaning "seeking" or "one who seeks". This adds a human element to our speculative stack, repositioning the user as an _active seeker_ of knowledge rather than a passive recipient. 

The Humus database could now be seen as storing not just decaying data, but the residual energy or intentions of past querents. This adds a layer of collective memory to the system, where past queries influence future interactions in subtle ways.

Implementing a "decay function" in Humus (LOL) that not only forgets less-accessed data but also blends or mutates interpretations over time, creating new, emergent meanings.

A "digital patina" in Humus, where the decay process leaves visible traces that influence future interpretations; a "heat map" of the tarot deck, showing which cards and interpretations have been most influential over time?

- [?] Could we implement a system where frequently accessed Querent interpretations leave stronger "traces" in the database, influencing future readings more heavily?
- [?] Are we looking at an experimental platform for exploring new forms of human-computer interaction and digital meaning-making? What are the limitations of the "platform" metaphor, as opposed to a "digital ecosystem"/"noetic garden" evolving through use?
- [?] How could the system could be designed as a tool for expression and/or brainstorming, using the interplay of decay, active interpretation, and reparative dialogue to inspire new ideas?

[^1]: (J) Incorporate an idea of "forced first-perspective-taking" by prompting users to imagine themselves within the card imagery.
[^2]: (J) Implementing a "decay gradient" where frequently accessed or querent-modified interpretations decay more slowly?
[^3]: (J) Include visual representations of the cards alongside textual interpretations. Implement a feature to highlight specific symbols, colours, or characters in the card imagery as prompts for user intuition. Allow users to add, edit, group, and link attributes as they explore associations.