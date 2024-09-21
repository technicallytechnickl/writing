---
title: The Impact of Changing Requirements
layout: post
---

Requirements are the foundation of a product. All development is based on the requirements as documented.  Therefore, changes to the requirements are foundational changes that must be carefully considered.  

Changes to requirements can be intentional or circumstantial. Intentional changes to requirements can have many origins, but the shared characteristic is that someone made a decision to change what the product should do or how it should be built. Intentional changes usually have the advantage of being known beforehand and allow time for planning.  Circumstantial changes may not be obvious at all, and must be identified as soon as possible. Circumstantial changes are often due to external factors like a new competitor, customer dynamics changing, or major societal shifts like those caused by COVID.

Early requirements changes can have zero impact. If the requirement hasn't been considered yet or if the architecture is still fluid enough to accommodate the change, then it effectively didn't change anything. Early requirements changes can even be huge changes and remain free of change cost.  

On the flip side, late changes can create a need for a complete rebuild. Usually this manifests as a hack to the architecture though. These deep hacks create a cascade of issues in performance, support-ability, or flexibility throughout the rest of the life of the product. Even a minor word change in a single line of a contract can cause a huge ripple through an existing product. 

This dynamic is one reason that it is good to keep a flexible design and architecture even years into a product's development. The cost of maintaining the flexible architecture can pay itself back many times with a single unforeseen change. 

An example of keeping a flexible architecture 