# Speaker notes: Francesco's sections

Slide numbers are the ones printed in the footer of `latex_praesentation/main.pdf`.
Estimated: about 25 minutes (9.5 + 11 + 4.5).

Notation used in the deck: latents `U`, observations `X = f(U)`, graph `G`. The additional paper writes `V` for the latents and `U` for the noise; say this once on slide 17.

## Section 3: setup shared by both papers (about 9.5 min)

### Slide 10: Hard and soft interventions (2 min)
- An intervention changes one conditional distribution and leaves the others alone. This "sparse change" is the whole learning signal.
- Hard (perfect): the target is cut off from its parents. Example: a gene knock-out, or a randomised treatment.
- Soft (imperfect): the arrow stays, the mechanism changes. Example: shifting the mean, CRISPR activation.
- Hard is a special case of soft, so results for soft interventions are stronger in this respect.
- Both papers assume one target per intervention.

### Slide 11: Unpaired environments with unknown targets (1.5 min)
- We get one dataset per intervention plus the observational one.
- What is shared: the mixing `f` and all mechanisms that are not targeted. Without something shared, several datasets would not help.
- Unpaired: we never see the same cell before and after. Earlier work (Brehmer et al.) needed such counterfactual pairs.
- Unknown targets: the dataset label is known, the latent it acts on is not. This is realistic, since the latents themselves are unknown.

### Slide 12: Faithfulness (1.5 min)
- Markov goes from graph to distribution; faithfulness is the way back: every independence we see comes from the graph.
- Example on the slide: two paths that cancel exactly make a cause look independent of its effect. Faithfulness forbids this.
- It fails only for fine-tuned parameters, so it is a genericity assumption, like the "no fine-tuning" condition that appears later (slide 22).
- von Kügelgen et al. assume it for the latent distribution and use it in the last step of the proof to get the graph.
- Zhang et al. use versions adapted to interventions and to mixing. Do not state them: Joan covers the intuition.

### Slide 13: Why observational data is not enough (2 min)
- First layer: even with observed variables, the direction of an edge is not identifiable from i.i.d. data.
- Second layer: every latent can be rewritten as a function of independent noise, so "independent latents, empty graph" is always an alternative explanation. This is the non-identifiability of non-linear ICA.
- The main paper says the same: any DAG can explain the observational distribution.
- Punchline: what makes the causal variables special is that interventions act on them one at a time.

### Slide 14: What is the best we can hope for? (1.5 min)
- Relabeling and rescaling can always be undone inside `f`, so no data can remove them.
- The two papers aim at the same kind of statement, with a slightly different class: any monotone rescaling versus affine rescaling.
- Transition: one recap slide, then the paper that assumes nothing on `f`.

### Slide 15: Common ground (1 min)
- Recap of what both papers assume: latent DAG model, nonparametric mechanisms, a deterministic invertible mixing shared by all environments, a faithfulness-type assumption.
- Same data in both: unpaired, single-node interventions, unknown targets, every latent intervened on at least once, infinite data.
- Differences to keep in mind for what follows: class of mixing functions, hard versus soft, known or unknown number of latents.

## Sections 4 and 5: additional paper, von Kügelgen et al. (about 11 min)

Section 4 is the setup (slides 17-18), section 5 the result and ideas (slides 20-24).

No theorem statements or assumption lists here: only the model and the two ideas.

### Slide 17: Setting (1 min)
- Say the notation remark: their `V` is our `U`.
- On top of the common ground: arbitrary mechanisms and any smooth invertible mixing.
- The price: interventions must be hard, and the number of latents is known.
- Earlier work needed paired data, known targets, or linear/polynomial models.

### Slide 18: What does it mean to recover the model? (1.5 min)
- We learn an encoder and a graph. Success: each learned variable is exactly one true variable up to its scale, and the graphs match.
- Use the picture: names and scales may differ, the structure is the same.
- This is the best one can get from interventional data.
- Although scale is arbitrary, the strength of each arrow is the same in every solution.

### Slide 20: Main result (2 min)
- Two latents: three datasets are enough, observational plus one hard intervention on each latent.
- Any number of latents: two different hard interventions on each latent, and we know which two datasets form a pair.
- No restriction on the mixing or on the mechanisms, only "nothing is fine-tuned".
- Pairs of datasets (two doses), not pairs of samples.

### Slide 21: Idea 1, compare environments (2 min)
- Two environments differ in one mechanism. Dividing the densities cancels everything they share.
- The ratio is a function of the intervened variable alone.
- The learned model must show the same ratio, so one learned variable corresponds to one true variable.
- The sparse change between environments is the whole learning signal; the shape of `f` plays no role.

### Slide 22: The difficulty, unknown targets (1.5 min)
- Walk through the figure: in `e1` the truth intervenes on node 1, the model says node 2.
- This case is what makes the problem hard and is new in this paper.
- It can only happen if the mechanisms are fine-tuned to each other; generic models exclude it. Link back to faithfulness (slide 12).

### Slide 23: Idea 2, why hard interventions (1.5 min)
- A wrong representation could add a function of the parent to the child.
- After a hard intervention the child is independent of the parent, so this mixing would be detected.
- After a soft intervention the child still depends on the parent, so the mixing cannot be detected.
- This is the hook for the limitations and for the main paper.

### Slide 24: Experiment (1.5 min)
- Small synthetic check with two latents: one model per graph and target assignment.
- Right panel: misspecified models usually fit worse, so the likelihood can select graph and targets.
- Left panel: only the correct model recovers the latents.
- This is a search over all candidates: fine for two nodes, not beyond.

## Section 6: limitations and motivation (about 4.5 min)

### Slide 26: Limitations (2 min)
- Perfect interventions only, while CRISPR activation and drugs are soft.
- Known number of latents.
- Paired interventions for more than two latents.
- No scalable algorithm, and only toy experiments.
- The authors themselves name soft interventions as future work.

### Slide 27: Side by side (1.5 min)
- Read the red cells only: polynomial mixing, soft interventions, number of latents learned, a VAE-based algorithm.
- Same in both: nonparametric mechanisms, unknown targets, unpaired data.
- The last row shows the difference in scale.

### Slide 28: Motivation and hand-over (1 min)
- The main paper restricts the mixing and accepts that single latents are not recovered one by one.
- In exchange: soft interventions, unknown `p`, one intervention per node, and a method for real data.
- Hand over to Joan with the question on the slide.
