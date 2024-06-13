# Working Notes 2: Roughing Out an EAV Data Model

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

[?] How would Ian Bogost handle this? He is interested in how things interact and experience each other, beyond human comprehension. He would approach the tarot cards and their meanings as "aliens": objects/entities in their own right.

## A couple of examples:

### 0. The Fool

> "0 - The Fool": "Beginnings, innocence, spontaneity. The eternal child, filled with wonder and trust in the universe. Embarking on a new adventure with a free spirit and faith in the future."

{"0 - The Fool": {  
&nbsp;&nbsp;&nbsp;&nbsp;"arcanum": "Major"[^1],  
&nbsp;&nbsp;&nbsp;&nbsp;"keywords": ["Beginnings", "Innocence", "Spontaneity"][^2],  
&nbsp;&nbsp;&nbsp;&nbsp;"description": "The eternal child, filled with wonder and trust in the universe. Embarking on a new adventure with a free spirit and faith in the future."[^3],  
&nbsp;&nbsp;&nbsp;&nbsp;"archetype": "The eternal child"[^4],  
&nbsp;&nbsp;&nbsp;&nbsp;"action": "Embarking on a new adventure"[^5],  
&nbsp;&nbsp;&nbsp;&nbsp;"emotion": ["wonder", "trust"][^6],  
&nbsp;&nbsp;&nbsp;&nbsp;"characteristics": ["eternal child", "free spirit", "faith in the future"][^7] }  
}  

### 1. The Magician

> "1 - The Magician": “Manifestation, resourcefulness, power. The visionary, skillfully wielding the tools of creation. Turning dreams into reality through willpower and inspired action.”

{"1 - The Magician": {  
&nbsp;&nbsp;&nbsp;&nbsp;"arcanum: "Major",  
&nbsp;&nbsp;&nbsp;&nbsp;"keywords": ["Manifestation", "Resourcefulness", "Power"],  
&nbsp;&nbsp;&nbsp;&nbsp;"description": "The visionary, skillfully wielding the tools of creation. Turning dreams into reality through willpower and inspired action.”,  
&nbsp;&nbsp;&nbsp;&nbsp;"archetype": "The visionary",  
&nbsp;&nbsp;&nbsp;&nbsp;"action": ["wielding the tools of creation", "turning dreams into reality"]  
&nbsp;&nbsp;&nbsp;&nbsp;"entities": ["The tools of creation", "willpower"][^8],  
&nbsp;&nbsp;&nbsp;&nbsp;"emotion": "inspired",  
&nbsp;&nbsp;&nbsp;&nbsp;"characteristics": ["visionary", "skillful", "inspired"] }  
}  

### 2. The High Priestess

> "2 - The High Priestess": "Intuition, mystery, the subconscious mind. The guardian of hidden knowledge, sitting between the pillars of duality. Trusting in wisdom that comes through stillness and dreams."

{"2 - The High Priestess": {  
&nbsp;&nbsp;&nbsp;&nbsp;"arcanum: "Major",  
&nbsp;&nbsp;&nbsp;&nbsp;"keywords": ["Intuition", "Mystery", "The subconscious mind"],  
&nbsp;&nbsp;&nbsp;&nbsp;"description": "The guardian of hidden knowledge, sitting between the pillars of duality. Trusting in wisdom that comes through stillness and dreams.",  
&nbsp;&nbsp;&nbsp;&nbsp;"archetype": "The guardian of hidden knowledge",  
&nbsp;&nbsp;&nbsp;&nbsp;"action": ["sitting between the pillars of duality", "trusting in wisdom that comes through stillness and dreams"],  
&nbsp;&nbsp;&nbsp;&nbsp;"entities": "The pillars of duality"[^9],  
&nbsp;&nbsp;&nbsp;&nbsp;"emotion": "trusting",  
&nbsp;&nbsp;&nbsp;&nbsp;"characteristics": ["guardian", "still"] }  
}  

[^1]: Should any/all of these attributes be singular or plural?
[^2]: I think the LLMs have provided three primary keywords for each card, which is handy. Need to look into the etymology and origins of "keyword", as a label. If these are immutable features, it'd be good to have them as something we can focus in on, and that user-querent annotations can get stuck to.
[^3]: All of the provided interpretation string, minus the initial keywords/themes.
[^4]: Is there only ever one archetype for each card? Is the titular entity also an entity, distinct from the card object? Do we need to distinguish between The Fool (the Major Arcanum) and The Fool (the depicted, eponymous entity)? What would it be like if we _didn't_, ontologically?
[^5]: Verbs, basically.
[^6]: Trickier. What is the emotion attached to? Is the emotion a property of the card, the archetype, a given entity, or an action? I guess we're aiming for a flat ontology, where it's just kind of floating around in the general vicinity, as more of an _atmosphere_.
[^7]: Difference between emotion and characteristics might be tricky, even if these are qualities of the card-entity.
[^8]: Can an attribute of an entity be an entity? Entityception. I _think_ "the tools of creation" makes sense here. "Willpower" might not.
[^9]: I'm assuming this doesn't need to be: `"entitites": ["One of the pillars of duality", "The other pillar of duality"]`, but who knows.