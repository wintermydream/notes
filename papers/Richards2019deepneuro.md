# A deep learning framework for neuroscience

Richards, B. A., Lillicrap, T. P., Beaudoin, P., Bengio, Y., Bogacz, R., Christensen, A., ... & Gillon, C. J. (2019). A deep learning framework for neuroscience. Nature neuroscience, 22(11), 1761-1770.
[Direct link shared by Blake](https://www.nature.com/articles/s41593-019-0520-2.epdf?shared_access_token=n1zyUZ6-ypeHWkeaEs1FPNRgN0jAjWel9jnR3ZoTv0N5dsTXXcjpcGP7i54eL_L9GTMgy1V6NUDPE4-SxE_8Ip1gIa5G35VU4LeqRZ56IGy5uMJKd6aUZ4JeYonqPfWkstTCNFgazGPl8xJGrQAvuw%3D%3D)

#review #deepneuro #bib #credit

Parent: [[12_Neuro]]

Full list of authors: 
Blake A. Richards, Timothy P. Lillicrap, Philippe Beaudoin, Yoshua Bengio, Rafal
Bogacz, Amelia Christensen, Claudia Clopath, Rui Ponte Costa, Archy de Berker, Surya Ganguli, Colleen J. Gillon, Danijar Hafner, Adam Kepecs, Nikolaus Kriegeskorte, Peter Latham, Grace W. Lindsay, Ken Miller, Richard Naud, Christopher C. Pack, Panayiota Poirazi, Pieter Roelfsema, João Sacramento, Andrew
Saxe, Benjamin Scellier, Anna Schapiro, Walter Senn, Greg Wayne, Daniel Yamins, Friedemann Zenke, Joel Zylberberg, Denis Therien, Konrad P.Kording

That impactful opinion piece with 20 or something coolest comp neuroscientists. Overall, a great review to cite every time you claim that "bottom-up then compare" is a more productive approach for reverse engineering complex systems than going "top-down".

Success stories for "few neurons recordings": CPGs, VOR, motion in the retina. With many neurons, this doesn't work, but maybe ANNs will help.

For ANNs, 3 components that aren't learned:
* Objective function (or loss)
* Learning rules (update rule)
* Architecture

A one-link-for-each review of what deep learning can do. Followed by a list of what brain things were replicated with deep learning: grid cells, shape tuning, temporal receptive fields, visual illusions, apparent model-based reasoning.

In the blue box: a summary of backprop, and ~10 links to various potential solutions for **credit assignment** that estimate gradient, but are more biologically plausible. Fig 2 roughly classifies all these methods on their Bias / Variance performance (most for now have high variance rather than high bias). If interested in credit assignment, this part should be harvested for links.

"No free lunch theorems": different problems require different learning rules. "AI set": a hypothesis that those things that animals do well, should be "easy" for neural networks. However animals have strong inductive biases (see Zador's recent opinion), and similarly humans have to fine-tune ANN architectures for the task. And still this is better than tuning neurons by hand, as everything boils down to "3 components" outlined above, even tho it means no low-level interpretability. Compare brain development to evolution: we know the rules, but not the result.

How to reverse-engineer objective functions for the brain? Sometimes from common sense (e.g. predictive coding = optimize description length). Box with more examples: log-probability of action sequences scaled by the reward they have produced; increase of mutual information with the environment ("empowerment" - apparently a term!) Also a quick plug for "learning how to learn". Ultimately, we need behavior / ethology to guess the objective functions (*they mention brain-machine interfaces, but virtual environments Engert-style would actually be kinda more in spirit*)

How to use this approach? Create models that solve the task; make predictions; compare with the brain. Link plasticity rules to representations, and the other way around (ref 77: Lim2005).

Interesting point: most past comp neuro work was done on brain dynamics, and this new proposal doesn't quite interact with that past work. 

> They sorta brush this last statement off, but maybe that's just because we (humans) know and like DL right now, so DL becomes a good metaphor that we try to apply to the brain, even though the brain is mostly recurrent. Maybe when (if) we understand recurrent networks better, and depart from the DL paradigm, dynamics would be easily plugged into this framework as well? As yet another readout, similar to connectivity, that can be rebuilt bottom-up, then verified?