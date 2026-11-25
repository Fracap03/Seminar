# Speaker notes: Francesco's sections

Slide numbers are the ones printed in the footer of `latex_praesentation/main.pdf`.
Estimated: about 24.5 minutes (9 + 11 + 4.5).

Notation used in the deck: latents `U`, observations `X = f(U)`, graph `G`. The additional paper writes `V` for the latents and `U` for the noise; say this once on slide 22.

## Section 3: setup shared by both papers (about 9 min)

Joan introduces why the problem exists (including the ICA comparison, slide 5, and hard/soft interventions, slide 9). This section says which conditions allow solving it: the data; what links the datasets; the formal identification question; Markov and faithfulness; the two setups compared.

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
- Recall Markov here, in one sentence: the factorization is what the graph implies for the distribution. Do not introduce d-separation (backup slides in the appendix).

### Slide 18: The formal identification question (1.5 min)
- Joan showed intuitively why names and scales stay ambiguous (slide 8). Here we make the question precise.
- A candidate is an encoder plus a graph. It must explain all environments and respect the assumptions: the dashed set.
- Harmless candidates (renamed, rescaled) form the blue class. The red one is really wrong: latents mixed, arrow reversed, same data.
- The question: do all compatible candidates belong to the blue class? If yes, the model is identified, up to equivalence.
- A theorem must say what is recovered (factors, graph, targets) and up to which transformations. The guarantees are about exactly known distributions, not about the optimization succeeding.
- Transition, say it explicitly: "Compatibility with the data is not enough without assumptions that link the distribution to the causal structure. Let us look at this link." The next slide is that link.

### Slide 19: Can independence hide causal connections? (1.5 min)
- The slide builds in three steps; one problem only, and the reason for the assumption.
- Say: "From the first node two contributions reach the third: an indirect positive one and a direct negative one. Here they cancel exactly. So in the data we find independence, although the graph has connections. Faithfulness excludes these coincidences: we want independences to reflect the structure of the graph."
- Then the comparison: the additional paper assumes standard faithfulness; the main paper uses distinct conditions for interventions and linear mixing. They are not the same assumption.

### Slide 20: Two routes to identifiability (1 min)
- The two papers choose different trade-offs between flexibility of the mixing, experimental information and strength of the identification.
- Read the table by rows: mixing, interventions, number of latents, what is recovered.
- Transition: this introduces the additional paper, the one with the general mixing.

## Moved to Joan's introduction

### Slide 5: From independent components to causal variables (2 min)
- ICA looks for independent factors, we look for causally related factors and their graph.
- Put the two problems side by side: same mixing, same observations; the only difference is whether the latents have edges.
- With an empty graph the causal factorization is a product of marginals: our problem is exactly nonlinear ICA. So this setting generalizes ICA.
- The other direction is the warning: any causal model can be rewritten with independent noise and a bigger mixing, so an ICA method would return the noise with an empty graph.
- This is the "spurious ICA solution" of the additional paper, and the reason interventions on the causal variables are needed.
- Do not quote a number of environments needed by nonlinear ICA: it depends on the specific result.

## Sections 4 and 5: additional paper, von Kügelgen et al. (about 11 min)

Section 4 is the setup (slides 22-23), section 5 the result and ideas (slides 25-29).

No theorem statements or assumption lists here: only the model and the two ideas.

### Slide 22: Setting (1 min)
- Say the notation remark: their `V` is our `U`.
- On top of the common ground: arbitrary mechanisms and any smooth invertible mixing.
- The price: interventions must be hard, and the number of latents is known.
- Earlier work needed paired data, known targets, or linear/polynomial models.

### Slide 23: What does it mean to recover the model? (1.5 min)
- We learn an encoder and a graph. Success: each learned variable is exactly one true variable up to its scale, and the graphs match.
- Use the picture: names and scales may differ, the structure is the same.
- This is the best one can get from interventional data.
- Although scale is arbitrary, the strength of each arrow is the same in every solution.

### Slide 25: Main result (2 min)
- Two latents: three datasets are enough, observational plus one hard intervention on each latent.
- Any number of latents: two different hard interventions on each latent, and we know which two datasets form a pair.
- No restriction on the mixing or on the mechanisms, only "nothing is fine-tuned".
- Pairs of datasets (two doses), not pairs of samples.

### Slide 26: Idea 1, compare environments (2 min)
- Two environments differ in one mechanism. Dividing the densities cancels everything they share.
- The ratio is a function of the intervened variable alone.
- The learned model must show the same ratio, so one learned variable corresponds to one true variable.
- The sparse change between environments is the whole learning signal; the shape of `f` plays no role.

### Slide 27: The difficulty, unknown targets (1.5 min)
- Walk through the figure: in `e1` the truth intervenes on node 1, the model says node 2.
- This case is what makes the problem hard and is new in this paper.
- It can only happen if the mechanisms are fine-tuned to each other; generic models exclude it. Link back to faithfulness (slide 19).

### Slide 28: Idea 2, why hard interventions (1.5 min)
- A wrong representation could add a function of the parent to the child.
- After a hard intervention the child is independent of the parent, so this mixing would be detected.
- After a soft intervention the child still depends on the parent, so the mixing cannot be detected.
- This is the hook for the limitations and for the main paper.

### Slide 29: Experiment (1.5 min)
- Small synthetic check with two latents: one model per graph and target assignment.
- Right panel: misspecified models usually fit worse, so the likelihood can select graph and targets.
- Left panel: only the correct model recovers the latents.
- This is a search over all candidates: fine for two nodes, not beyond.

## Section 6: limitations and motivation (about 4.5 min)

### Slide 31: Limitations (2 min)
- Perfect interventions only, while CRISPR activation and drugs are soft.
- Known number of latents.
- Paired interventions for more than two latents.
- No scalable algorithm, and only toy experiments.
- The authors themselves name soft interventions as future work.

### Slide 32: Side by side (1.5 min)
- Read the red cells only: polynomial mixing, soft interventions, number of latents learned, a VAE-based algorithm.
- Same in both: nonparametric mechanisms, unknown targets, unpaired data.
- The last row shows the difference in scale.

### Slide 33: Motivation and hand-over (1 min)
- The main paper restricts the mixing and accepts that single latents are not recovered one by one.
- In exchange: soft interventions, unknown `p`, one intervention per node, and a method for real data.
- Hand over to Joan with the question on the slide.
