# SVM - Support Vector Machine

#classification

Parent: [[03_Classification]]
Related: [[logreg]]

**General idea:** widest street approach: find a line, so that if you have a band around the line, it separates the positive from the negative examples as best as possible. If the line is described with a normal vector ω ⊥ line, whether a point x is far from the line can be described as ⟨x , ω⟩. If b is a good threshold value for this product (if we get b when x lies right smack on the separating line), we have xᵀω + b ≥ 0. To find the best line, let's try to find ω and b, so that for positive samples we would get xᵀω+b>1 (not just >0), and for negative samples, xᵀω+b<-1. 

We have already seen linear separators f(x) = xᵀθ = 0 before (see [[logres]]). The hyperplane (line in 2D) it defines is ⊥ to θ, and f(x) is proportinal to the distance from x to the plane.

**Rosenblatt's Perceptron** from 1958:  tries to minimize distances from misclassified points to the boundary: D = -∑y(xᵀθ) ≥ 0. This assumes that most y=1 lie beyond the boundary, so if y=1 is left closer to 0 its positive y gets multiplied by a negative xθ, resulting in a negative value; thus - before the sum. The original perceptron used stochastic gradient descent, visiting points one by one, and setting θ := θ + αyx (as usual, assuming that x0=1 and θ_0 is intercept). Obvious problems: non-deterministic, slow, doesn't converge for non-separable data (instead, cycles with very slow cycles).

To make it more robust, let's maximize $M =\min_i(y_i x_i θ))$: maximize the smallest distance from a (correctly classified) point to the boundary. Aka "maximal separation", or **Optimally Seprating Hyperplanes**. Here θ is constrained to be unitary: $\sum_{i=1}^p θ^2_i = 1$. Note that here summing goes from 1, and not from 0: it is the actual "vector part" of θ that is normal (direction), while the intercept $θ_0$ is not bound (we need to be able to move the hyperplane arbitrarily in space). 

> ESL always writes y_i(x_i ᵀ β + β0), but that's annoying, isn't it? Other textbooks  just introduce special notation with a wave $\tilde θ$ for (θ1 … θp) sub-vector, and use θ for a full vector ([ref](https://www.dbs.ifi.lmu.de/Lehre/MaschLernen/SS2014/Skript/SupportVectorMachine2014.pdf)).

Instead of writing the constraint on θ explicitly, we can write the equation for an arbitrary θ that got normalized by its upper part: y(xᵀθ)/norm(θ) ≥ M for ∀(x,y); then move norm(θ) to the right: yxᵀθ ≥ M∙norm(θ); then assume that instead of norming to 1 we'll be norming to 1/M, so that M∙norm(θ)=1. Now instead of maximizing M, se can minimize the norm of upper part of θ: 

Optimize θ, to achieve $\min ||\tilde θ||$, provided that $y_i ⟨x_i , θ⟩ ≥ 1 \quad ∀i$. 

(Here, as in the prev paragraph, norm($\tilde θ$) is understood in terms of θ_1 to θ_p, excluding $θ_0$. The value 1/norm(θ) is called **thickness** of the decision boundary. Yields a convex problem with linear constraints, solvable with Lagrange optimization: L = |θ|² - ∑ λi ( yi ⟨x_i , θ⟩  - 1)…

> At this point (ESL p133) I give up for now. It seems that math around p134 is not how SVMs are actually implemented anyways, so it can probably wait. I'll rivisit this once I read the actual SVM chapter.

SVMs are very popular with **Kernel tricks**, such as radial basis kernel [[RBF]], as it produces simple yet expressive models ([ref](https://towardsdatascience.com/support-vector-machines-svm-c9ef22815589)).

# Refs
[A reasonable post abut SVM, by Ajay Yadav](https://towardsdatascience.com/support-vector-machines-svm-c9ef22815589)