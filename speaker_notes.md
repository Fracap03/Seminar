# Speaker notes: Francesco's sections

Slide numbers are the ones printed in the footer of `latex_praesentation/main.pdf`.
Estimated: about 29.5 minutes (14 + 11 + 4.5). To get back to 25, go quickly through slides 13-16 and 19-21.

Notation used in the deck: latents `U`, observations `X = f(U)`, graph `G`. The additional paper writes `V` for the latents and `U` for the noise; say this once on slide 26.

## Section 3: setup shared by both papers (about 14 min)

Hard and soft interventions are introduced by Joan (slide 8). The section follows six steps: from ICA to causal variables; the data; what links the datasets; what identification means; Markov and faithfulness; the two setups compared.

### Slide 11: From independent components to causal variables (2 min)
- Opening of the section: ICA looks for independent factors, we look for causally related factors and their graph.
- Put the two problems side by side: same mixing, same observations; the only difference is whether the latents have edges.
- With an empty graph the causal factorization is a product of marginals: our problem is exactly nonlinear ICA. So this setting generalizes ICA.
- The other direction is the warning: any causal model can be rewritten with independent noise and a bigger mixing, so an ICA method would return the noise with an empty graph.
- This is the "spurious ICA solution" of the additional paper, and the reason interventions on the causal variables are needed.
- Do not quote a number of environments needed by nonlinear ICA: it depends on the specific result.

### Slide 12: The environments (1 min)
- An environment is one experimental condition, with its own dataset.
- One is observational: nothing is touched. Each of the others comes from one intervention.
- Example: unperturbed cells, cells with gene A activated, cells with gene B activated.
- The next three slides say what we know and do not know about these datasets.

### Slides 13-15: Multi-environment data, one property per slide (2.5 min in total)
- Slide 13, unpaired samples: sequencing destroys the cell, so a cell is seen either unperturbed or perturbed. We compare populations, never the same unit before and after.
- Slide 14, known environment label: the experiment records which perturbation each cell received (in CRISPR screens via a barcode), so we know which experiment each sample comes from.
- Slide 15, unknown latent target: we know which gene the experiment activates, but not which hidden causal coordinate (gene program) that changes. Each row of the table is one cell. Stress the difference between knowing the experiment and knowing the target.

### Slides 16-17: Shared mechanisms and single-node interventions (2 min)
- This is what links the datasets. Without something shared, several datasets would not help.
- Slide 16: the mixing is the same in all environments.
- Slide 17: one mechanism is replaced per intervention, all the others stay the same. Read the chain example: only the red factor changes.
- One mechanism is changed directly, but many descendants can change in distribution.
- That every latent node is targeted is an assumption, not something we can check.

### Slide 18: What does identification mean? (1.5 min)
- A candidate is an encoder plus a graph. It must explain all environments and respect the assumptions. Many candidates explain the data: the dashed set.
- Some of them are harmless: renaming and rescaling the latents, as Joan showed. They form the blue set.
- Others are really wrong: here the latents are mixed and the arrow is reversed, yet the data are the same.
- Identification means the two sets coincide: every model that fits is equivalent to the truth.
- A theorem must say what is recovered (factors, graph, targets) and up to which transformations.
- Say aloud: the guarantees are about exactly known distributions, not about the optimization succeeding.
- Bridge: to link distributions and graph we need conditions that exclude accidental independences. That is the next step.

### Slides 19-21: d-separation, one structure per slide (2 min in total)
- d-separation is a purely graphical rule: it says when a set of nodes blocks all paths between two others. On each slide: left without conditioning, right conditioning on the middle node (shaded).
- Slide 19, chain: open by default, blocked when we condition on the middle node.
- Slide 20, fork: same behaviour. The middle node is a common cause.
- Slide 21, collider: the opposite. Blocked by default; it opens when we condition on the middle node or one of its descendants. The middle node is a common effect.
- Definition on slide 21: two nodes are d-separated by a set if every path between them is blocked.

### Slide 22: The Markov property (1 min)
- The graph implies independences in the distribution: separation in the graph gives conditional independence.
- Chain example: `U2` blocks the path, so `U1` and `U3` are independent given `U2`. This is the same as the factorization.

### Slide 23: Faithfulness (1.5 min)
- Faithfulness is the way back: every independence we see comes from the graph.
- Example: direct and indirect path cancel exactly when `c = -ab`, so a cause looks independent of its effect.
- The additional paper assumes standard faithfulness.
- The main paper uses specific conditions against cancellations under interventions and linear mixing. Say clearly that these are not the same assumption.

### Slide 24: Different assumptions, different guarantees (1 min)
- Read the table by rows: mixing, interventions, number of latents, what is recovered.
- One sentence to remember: the more general the mixing, the stronger the interventions must be.
- Transition: this introduces the additional paper, the one with the general mixing.

## Sections 4 and 5: additional paper, von Kügelgen et al. (about 11 min)

Section 4 is the setup (slides 26-27), section 5 the result and ideas (slides 29-33).

No theorem statements or assumption lists here: only the model and the two ideas.

### Slide 26: Setting (1 min)
- Say the notation remark: their `V` is our `U`.
- On top of the common ground: arbitrary mechanisms and any smooth invertible mixing.
- The price: interventions must be hard, and the number of latents is known.
- Earlier work needed paired data, known targets, or linear/polynomial models.

### Slide 27: What does it mean to recover the model? (1.5 min)
- We learn an encoder and a graph. Success: each learned variable is exactly one true variable up to its scale, and the graphs match.
- Use the picture: names and scales may differ, the structure is the same.
- This is the best one can get from interventional data.
- Although scale is arbitrary, the strength of each arrow is the same in every solution.

### Slide 29: Main result (2 min)
- Two latents: three datasets are enough, observational plus one hard intervention on each latent.
- Any number of latents: two different hard interventions on each latent, and we know which two datasets form a pair.
- No restriction on the mixing or on the mechanisms, only "nothing is fine-tuned".
- Pairs of datasets (two doses), not pairs of samples.

### Slide 30: Idea 1, compare environments (2 min)
- Two environments differ in one mechanism. Dividing the densities cancels everything they share.
- The ratio is a function of the intervened variable alone.
- The learned model must show the same ratio, so one learned variable corresponds to one true variable.
- The sparse change between environments is the whole learning signal; the shape of `f` plays no role.

### Slide 31: The difficulty, unknown targets (1.5 min)
- Walk through the figure: in `e1` the truth intervenes on node 1, the model says node 2.
- This case is what makes the problem hard and is new in this paper.
- It can only happen if the mechanisms are fine-tuned to each other; generic models exclude it. Link back to faithfulness (slide 23).

### Slide 32: Idea 2, why hard interventions (1.5 min)
- A wrong representation could add a function of the parent to the child.
- After a hard intervention the child is independent of the parent, so this mixing would be detected.
- After a soft intervention the child still depends on the parent, so the mixing cannot be detected.
- This is the hook for the limitations and for the main paper.

### Slide 33: Experiment (1.5 min)
- Small synthetic check with two latents: one model per graph and target assignment.
- Right panel: misspecified models usually fit worse, so the likelihood can select graph and targets.
- Left panel: only the correct model recovers the latents.
- This is a search over all candidates: fine for two nodes, not beyond.

## Section 6: limitations and motivation (about 4.5 min)

### Slide 35: Limitations (2 min)
- Perfect interventions only, while CRISPR activation and drugs are soft.
- Known number of latents.
- Paired interventions for more than two latents.
- No scalable algorithm, and only toy experiments.
- The authors themselves name soft interventions as future work.

### Slide 36: Side by side (1.5 min)
- Read the red cells only: polynomial mixing, soft interventions, number of latents learned, a VAE-based algorithm.
- Same in both: nonparametric mechanisms, unknown targets, unpaired data.
- The last row shows the difference in scale.

### Slide 37: Motivation and hand-over (1 min)
- The main paper restricts the mixing and accepts that single latents are not recovered one by one.
- In exchange: soft interventions, unknown `p`, one intervention per node, and a method for real data.
- Hand over to Joan with the question on the slide.
