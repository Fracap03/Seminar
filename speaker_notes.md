# Speaker notes: Francesco's sections

Slide numbers are the ones printed in the footer of `latex_praesentation/main.pdf`.
Estimated: about 32 minutes (9 + 18.5 + 4.5): setup 4.5 min, results 14 min. This is well over 25: see the options in the hand-over.

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

## Sections 4 and 5: additional paper, von Kügelgen et al. (about 18.5 min)

Section 4 is the setup (slides 22-25), section 5 the result and ideas (slides 26-30).

No theorem statements or assumption lists here: only the model and the two ideas.

### Slide 22: Setup, from hidden variables to a learned representation (1 min)
- Read the picture left to right: hidden causal variables `U`, mixed by `f` into the observed data `X`, encoded by `h` into the learned representation `Z`.
- Two graphs: the true latent graph `G` on `U`, and the inferred graph `G'` on `Z`.
- Only `X` is observed. The question of the paper is when `Z` and `G'` match `U` and `G`.
- The purple arrow is `psi = f^-1 o h^-1`, the map from the learned variables back to the true ones (`U = psi(Z)`). It is unknown; the whole question is what `psi` can look like. If the model is identified, `psi` only renames and rescales the variables (the `phi` of slide 25).
- Notation remark: the paper writes `V` for our `U`.

### Slide 23: General assumptions, recall from the common setup (1 min)
- Question of the slide: under which assumptions do we study the problem?
- Four recalls, go through them fast: the latent SCM (each latent is a function of its parents and independent noise); the multi-environment data; what is shared between environments; one target per intervention.
- Faithfulness is not on the slide: mention it in one sentence (standard faithfulness, as on slide 19).

### Slide 24: General assumptions, additional paper (1 min)
- Same model, now what this paper adds.
- More general than the main paper: the mechanisms are unrestricted, and the mixing is any diffeomorphism onto its image.
- More restrictive: interventions must be perfect, and the number of latents is known.
- Earlier work needed paired data, known targets, or linear/polynomial models.

### Slide 25: What is the learning target? (1.5 min)
- This comes before the results on purpose: we must say what "identify" means.
- We cannot recover `U` exactly: the names and the scales of the latents are arbitrary.
- The target is the equivalence class: each learned variable is exactly one true variable, up to an invertible rescaling, and the graphs match after renaming.
- Use the picture: here the permutation swaps the two variables.
- This is the best one can get from interventional data, and the strength of each arrow is the same in every equivalent solution.

### Slide 27: Theorem 3.2, bivariate identifiability (2 min)
- Recall the general assumptions (slides 23-24) in one sentence; explain only the new ones.
- Setting: two latents, three environments: observational, one perfect intervention on each variable. We do not know which environment targets which variable.
- A1 is a regularity condition. A2 is the data requirement.
- A3, interventional discrepancy: the intervention really changes the mechanism, everywhere (the ratio is strictly monotone).
- A4, genericity: the ratio between intervened and original mechanism of `U2` does not have the same distribution in `e0` and `e1`. In the paper it is stated with a test function `phi`; this is the same thing. It is what excludes misaligned targets (slide 30).
- Result: any candidate that fits is CRL-equivalent to the truth.

### Slide 28: Proof strategy, eliminating cross-coordinate dependencies (1.5 min)
- `psi` is the map of slide 22. At the start it is an arbitrary diffeomorphism: each true latent may depend on both learned coordinates.
- Read the left matrix: rows are true latents, columns are learned coordinates. Blue entries are the allowed dependencies, red entries are mixing.
- The goal is the right matrix: red entries equal to zero, so each true latent depends on one learned coordinate only.
- Say aloud (it is no longer on the slide): the goal is to eliminate cross-coordinate dependencies, up to a permutation of the latent variables. The diagonal form is the aligned case after relabeling; in general CRL equivalence allows a permutation.

### Slide 29: Proof idea, eliminating the first off-diagonal entry (3 min, five clicks)
- This is the only step shown in full. Example `U1 -> U2`, comparing `e0` with the intervention on the root.
- The blue tags say where each assumption enters: A1 for the densities and their ratio, A2 for having `e0` and the intervention on the root, A3 for the last step.
- Start: change of variables; in the ratio of two environments the Jacobian cancels, because `psi` is shared.
- Click 2: the shared mechanism cancels too, because the intervention is atomic. What remains, `R1`, depends on `u1` only.
- Click 3: with aligned targets the same ratio on the learned side is `S1(z1)`.
- Click 4: the left side does not depend on `z2`; differentiate. A3 says `R1'` is never zero, so the derivative of `psi1` with respect to `z2` vanishes.
- Click 5: the upper-right entry of the Jacobian becomes zero. The lower-left one is still open.

### Slide 30: Completing the proof, which assumption is used where (1 min)
- Say that this is a sketch, and do not explain the remaining steps: only name the assumption each one uses.
- Upper-right entry: A1, A2, A3 (previous slide).
- Lower-left entry: A1 and A2, and here it matters that the intervention on the child is perfect. One sentence: this is the step that fails for soft interventions, which is what the main paper addresses. Do not claim perfect interventions are necessary in general.
- Misaligned targets: excluded by A4.
- Graph: faithfulness.
- If asked for details: the lower-left step uses that a monotone map between two one-dimensional distributions is unique.

### Slide 31: Theorem 3.4, arbitrary number of latent variables (2 min)
- Any number of latents, but the number is known.
- Two distinct perfect interventions per latent. We know which two environments form a pair, not which latent they target.
- Pairs of environments (e.g. the same experiment at two doses), not pairs of samples. No observational data needed.
- A3' compares the two intervened mechanisms of a pair.
- It is a sufficient condition; the authors conjecture one intervention per node is enough.
- No proof on the slides. If asked: it is the same density-ratio argument as for Theorem 3.2, applied to each pair of interventions; since every latent is covered and `psi` is invertible, `psi` is a permutation with one scalar map per coordinate.

### Slide 32: Interpreting causal representations (1.5 min, two clicks)
- Names and scales of the latents are arbitrary, so numerical effects cannot be read off. Which causal quantities survive?
- Step 1, left picture: remove the arrow from `Ui` to `Uj` by feeding `Uj` an independent copy of `Ui`, drawn from its marginal. The formula is the new mechanism of `Uj`.
- Step 2: the causal influence is the KL divergence between the original distribution and the one with the arrow removed. It is zero when removing the arrow changes nothing, and grows with the strength of the arrow.
- Click: Theorem 4.2. The value is the same in every CRL-equivalent representation: it does not change under element-wise invertible rescaling, and it follows the variables under permutation. No proof.
- Say aloud as conclusion: despite the unavoidable ambiguities, the learned graph keeps meaningful quantitative information.

### Slide 33: From identifiability to learning (1.5 min)
- The contribution is theoretical; the learning method is a proof of concept.
- Two proposals in the paper; the experiments use maximum likelihood.
- All four candidates see the same datasets. For each, graph and targets are fixed; a normalizing flow and the mechanisms are learned. No architecture details.
- Limitation: the search over graphs and targets does not scale.

### Slide 34: Experimental validation (1.5 min)
- Setting in one sentence.
- Right panel: difference in validation log-likelihood; the correct model is generally the best, so likelihood can select graph and targets.
- Left panel: MCC close to one only for the correct model.
- Read the last sentence as the transition to the limitations.

## Section 6: limitations and motivation (about 4.5 min)

### Slide 36: Limitations (2 min)
- Perfect interventions only, while CRISPR activation and drugs are soft.
- Known number of latents.
- Paired interventions for more than two latents.
- No scalable algorithm, and only toy experiments.
- The authors themselves name soft interventions as future work.

### Slide 37: Side by side (1.5 min)
- Read the red cells only: polynomial mixing, soft interventions, number of latents learned, a VAE-based algorithm.
- Same in both: nonparametric mechanisms, unknown targets, unpaired data.
- The last row shows the difference in scale.

### Slide 38: Motivation and hand-over (1 min)
- The main paper restricts the mixing and accepts that single latents are not recovered one by one.
- In exchange: soft interventions, unknown `p`, one intervention per node, and a method for real data.
- Hand over to Joan with the question on the slide.
