# GPT-2 and the nature of intelligence
The Gradient. 25 Jan 2020. Gary Marcus
https://thegradient.pub/gpt2-and-the-nature-of-intelligence/

#language #opinion #meaning #gi

An opinion piece on OpenAI's gpt2 model.

Starts with contrasting two schools of thought:
* Nativist (human mind isn't blank): Plato, Kant, Chomsky, Pinker, Elizabeth Spelke
* Empiricist (mostly learning): Locke

Then claims that GPT-2 may be a test. Can it learn to speak without being given an explicit Chomskian structure of language, from statistics only?

> To me, setting a split like that is an obvious recipe for disaster, just because post-Darwin, there is no longer a philosophical / metaphisical split here, but merely a practical one. Starts with the **peripathetic axiom** by Aristotle (promoted by Aquinas): "**There's nothing in the intellect that was not first in the senses**" ([ref](https://en.wikipedia.org/wiki/Peripatetic_axiom)). At the surface it is obviously untrue, as no animal is born without pre-configured architectures, reflexes, instincts, developmental priors, and what not. But at a deeper level, of course one can argue that no pre-packaged ability to see can develop (evolve) in a species that doesn't use vision, as otherwise it would not have mattered. So in a way it was in the experience, just not in the experience of this individual. Which is interesting and rich in its own way. But it totally shifts the problem. And obviously, makes any comparisons of animal (human) mind and AI rather complicated, as one has to always account both for personal history of learning, and the priors. A difference in the split may be important, or it may be irrelevant, depending on the question!

The author then states that GPT "is the antithesis to almost everything Noam Chomsky has argued about language", as in Chomskian system there's a pre-set tree of "universal grammar" that has pre-defined slots for, say, verbs (actions) and nouns (objectgs), and every sentence fits this tree to some degree, and is both generated by it, and intepreted via it. While GPT is just a bag of correlations.

> Which again shows either a perfect misunderstanding of the situation, or, more likely, a semi-intentional misinterpreatation. If Chomskian paradigms are present in the training dataset, in the sense of implicitly giving structure to every sentence in it, then the model is bound to learn it, as it would be an efficient way to compress (represent) this data. If there is structure, it will be discovered. So while DL models can be used a test for Chomskian hypothesis, it would not about whether (or how) they learns to interpret or generate language, but about how they represent it in their inner layers. Which probably may be directly observed (although it's not easy), and probably can also be tested.

Then he claims that transformers make no commitments to parts of speech.

> This is also questionable, for a yet different reason: the [[transformers]] model, used for GPT, is actually quite forced, in the sense that it is pretty far from a simple stack of dense layers that left to their own devices, developing inner representation. While this entire structure of Keys, Queries, and Values is not pre-set with noun-aspects and verb-aspects, it is clearly designed to seek representations like that. I do not have a good intuition for how much it can be considered Chomskian - both philosophically (to what degree you can be called Chomskian if you expect the universal grammar, but do not make statements about its structure?) and practically (how would a performance change if you encode Chomskian semantics directly). But it doesn't feel like Marcus's statement is as obvious as it seems.

Marcus admits later that "Of course, nothing can literally be a blank slate; true empiricism is a strawman", but quickly dismisses that, and claims that gpt is still "awfully close" to a tabula rasa. _Hmm, no._

Then tests gpt with a bunch of sentences that look like "I grew up in Athens. I speak fluent...", except that the name of the city is changed, and the model always follows with a correct language.

Second hypothesis: that sentences can be represented as vectors, and do not need complex trees. Marcus mostly describes it as Geoffrey Hinton's hypothesis.

> Again, doesn't feel fair. Everything may be encoded in a vector, including a value of any node in a tree, or the structure of a tree itself, It's how this vector is used, in the sence of interacting with the structure of the network, is that sets the non-linear aspects of transofrmations. Ultimately, it's all about non-linear aspects of it, isn't it? Vectors can be added and even averaged; with trees maybe you can add, to some degree, but averaging may quickly become problematic.

But then demonstrates with some good examples, such as counting objects from a narrative, the model fails spectacularly ("I put two trophies on a table, and then add another, the total number is..."). It cannot generalize too well. And then some other examples where one sentence introduces topic 1 with aspects 1 (such as place, or language), then another sentence introduces topic 2 with aspects 2, and a question about topic 1(or rather, seed, that is to be continuied) is answered with some mix of aspect 1 and aspect 2. Like super-priming, where you cannot hold 2 thoughts at the same time, but have them bleed into each other, and intertwine semantically.

> Which is not surprising, given the structure of the model. But this part is good: Marcus identified the weak points of this model really nicely!

Also it fails on syllogisms. Behaves as a Wernike aphasia patient.

Great quote: "This is why GPT-2 is so much better at writing surrealist prose than holding a steady line in nonfiction"