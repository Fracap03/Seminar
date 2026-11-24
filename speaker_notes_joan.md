# Speaker notes: Joan's introduction

Slide numbers are the ones printed in the footer of `latex_praesentation/main.pdf`.
Estimated: about 12.5 minutes for slides 2-9. "Step" means one click within a slide (the page number stays the same).

Notation: latents `U`, observations `X = f(U)`, graph `G`.

## Section 1: introduction (about 12.5 min)

### Slide 2: Why discovering causal structures is important? (1.5 min)
- Step 1, causal graph: air pressure causes both the barometer reading and the storm.
- Step 2: we push the needle up to high pressure, hoping to avoid the storm. The storm still comes.
- The reading predicts storms perfectly, but changing it changes nothing: air pressure causes both. A predictive model cannot tell you this; the causal graph can.
- The dashed edge: forcing the needle cuts its link to air pressure. This previews hard interventions (slide 8).
- Step 3: read the sentence. Discovering causal structure from observational and interventional data lets scientists answer causal questions.

### Slide 3: The variables we measure are rarely the causal ones (1.5 min)
- Step 1, images. Point at the red pixel `i`: same position in both images. Here it is ball, here it is sky. Same variable, completely different meaning.
- What we care about, where the ball is, is not any single pixel: it is spread over many of them. Repainting pixel `i` does not move the ball.
- Step 2, gene expression: more than 20,000 genes are measured per cell, genes in the same pathway act together, the causal variables are programs (groups of genes).
- If asked: unlike a pixel, gene `i` is the same gene in every cell. The problem is different: thousands of measured variables driven by a few hidden programs, whose genes are scattered.
- Step 3: causal variables need to be learned from data instead of taken for granted.

### Slide 4: Causal disentanglement (1.5 min)
- Say the other name once: this is also called causal representation learning.
- Step 1: a few latent variables, related by a directed acyclic graph (DAG). This is where "DAG" is defined.
- Step 2: an unknown mixing function `f` maps them to what we observe. "Mixing function" is the standard term (from ICA); some ML papers call it a decoder or generator.
- Step 3: the goal is to recover the latents and their graph from samples of `X`: the red "recover" arrow.

### Slide 5: Observing is not enough (2 min)
- Step 1: two models with opposite edges, `U1 -> U2` and `U2 -> U1`. The latents are hidden; we only see samples of `X`. Without interventions both models produce the same data (standard example: linear-Gaussian mechanisms give the same joint distribution, so the same `f` gives the same `X`).
- Step 2: intervene on `U1`. In model A the change reaches `U2`, so the cloud moves diagonally; in model B it does not, so the cloud moves sideways. We never look at `U`: the difference is in how the observed data move.
- Step 3: to recover the hidden graph, we need to see how `X` responds to interventions.
- Caveat if asked: here we assumed we know the intervention hits `U1`. In reality the target is unknown; handling that is part of what both papers do.
- Francesco's "Why observational data is not enough" uses the same two-model example: refer back to it, or agree beforehand.

### Slide 6: Problem setup (1.5 min)
- Step 1: the equation. `X = f(U)`, and the product means each latent is generated from its direct causes only (formally: `P_U` factorizes according to `G`, the causal Markov property).
- Say what was cut from the slide: `X` could be the expression of `n` genes; in practice `p` is much smaller than `n`; `f` can be non-linear. `f: R^p -> R^n` shows it is a map from `p` latents to `n` observations.
- Step 2, the unknowns: the latents, their number `p`, the graph, `f`, and which latent each intervention targets.
- Step 3, Figure 1 of the main paper: the abstract picture from slide 4, now with real data. The lightning bolts are interventions (more in two slides); the coloured row groups of the heatmap are the datasets from different interventions.

### Slide 7: Can we learn the latent model from the data? (2 min)
- The question follows from the "Unknown" box: can we recover all of this from data alone?
- Step 1: only if no other latent model explains the data equally well. Then the model is identifiable. Callback: the two models of slide 5 explained the same data, so that was a non-identifiable situation.
- Step 2: some changes can never be detected, because `f` absorbs them: permuting the latents, and an affine transform of each latent separately. Mixing latents (for example adding `U1` to `U2`) is not in this class.
- Hence the best possible result is identifiability up to an equivalence class.
- Steps 3-4, the figure: the right model swaps the names and doubles `U2`. With `f~(u1, u2) = f(u2, u1/2)` it produces exactly the same `X`. The graph has the same structure with new names, and interventions carry over, so no data of any kind can tell the two apart.
- Say once (removed from the slide): all statements are for infinite data, i.e. the distributions of `X` are known exactly.
- If asked about the class: von Kügelgen et al. allow any invertible map per latent; Zhang et al. (polynomial `f`) narrow it to affine maps.

### Slide 8: What does an intervention do? (1.5 min)
- Step 1: an intervention changes one conditional probability, the mechanism of its target, while all the others stay the same. This sparse change is the learning signal.
- Step 2, hard: the target no longer depends on its parents. Example: a gene knock-out, or the barometer needle on slide 2.
- Step 3, soft: changes the mechanism of the dependency; hard is a special case. Example: a shift of the mean; CRISPR activation.
- The dashed arrow here means "the link is still there, but its mechanism changed" (on slide 2 it meant a cut link): say this explicitly.
- Step 4: each intervention targets a single latent variable (atomic). Both papers assume this; it comes back as a limitation at the end.

### Slide 9: The question of this talk (1 min)
- Step 1: real perturbations are soft. Can they still reveal the latent causal model? CRISPR activations do not cut causal links, they change them.
- Step 2, additional paper (von Kügelgen et al.): no assumption on the mixing function, but needs hard interventions. A theory paper; experiments are small and synthetic.
- Step 3, main paper (Zhang et al.): polynomial mixing function, extends the theory to soft interventions and proposes a method to learn the model.
- Set expectations: with soft interventions, Zhang et al. recover the graph and the targets, not each latent on its own.
- Hand over to Francesco: first the setup shared by both papers.
