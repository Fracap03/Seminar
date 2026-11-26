# Speaker notes: Francesco's sections

Slide numbers are the ones printed in the footer of `latex_praesentation/main.pdf`.
Estimated: about 36 minutes (9 + 23.5 + 3.5): setup 5 min, results 18.5 min. This is well over 25: see the options in the hand-over.

Notation used in the deck: latents `U`, observations `X = f(U)`, graph `G`. Nonparametric Identifiability writes `V` for the latents and `U` for the noise; say this once on slide 22.

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
- Slide 15, unknown latent target: we know which gene the experiment activates, but not which hidden causal coordinate (gene program) that changes. Each row of the table is one cell, and an environment contains many cells; the values are made up, for illustration only. Stress the difference between knowing the experiment and knowing the target.

### Slides 16-17: Shared mechanisms and single-node interventions (2 min)
- This is what links the datasets. Without something shared, several datasets would not help.
- Slide 16: the mixing is the same in all environments.
- Slide 17: one mechanism is replaced per intervention, all the others stay the same. Read the chain example: only the red factor changes.
- One mechanism is changed directly, but many descendants can change in distribution.
- That every latent node is targeted is an assumption, not something we can check.
- Recall Markov here, in one sentence: the factorization is what the graph implies for the distribution. Do not introduce d-separation.

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
- Then the comparison: Nonparametric Identifiability assumes standard faithfulness; Causal Disentanglement uses distinct conditions for interventions and linear mixing. They are not the same assumption.

### Slide 20: Two routes to identifiability (1 min)
- The two papers choose different trade-offs between flexibility of the mixing, experimental information and strength of the identification.
- Read the table by rows: mixing, interventions, number of latents, what is recovered.
- Transition: this introduces Nonparametric Identifiability, the one with the general mixing.

## Moved to Joan's introduction

### Slide 5: From independent components to causal variables (2 min)
- ICA looks for independent factors, we look for causally related factors and their graph.
- Put the two problems side by side: same mixing, same observations; the only difference is whether the latents have edges.
- With an empty graph the causal factorization is a product of marginals: our problem is exactly nonlinear ICA. So this setting generalizes ICA.
- The other direction is the warning: any causal model can be rewritten with independent noise and a bigger mixing, so an ICA method would return the noise with an empty graph.
- This is the "spurious ICA solution" of Nonparametric Identifiability, and the reason interventions on the causal variables are needed.
- Do not quote a number of environments needed by nonlinear ICA: it depends on the specific result.

## Sections 4 and 5: Nonparametric Identifiability, von Kügelgen et al. (about 23.5 min)

Section 4 is the setup (slides 22-25), section 5 the result and ideas (slides 26-30).

No theorem statements or assumption lists here: only the model and the two ideas.

### Slide 22: Setup, from hidden variables to a learned representation (1 min)
- Read the picture left to right: hidden causal variables `U`, mixed by `f` into the observed data `X`, encoded by `h` into the learned representation `Z`.
- Two graphs: the true latent graph `G` on `U`, and the inferred graph `G'` on `Z`.
- Only `X` is observed. The question of the paper is when `Z` and `G'` match `U` and `G`.
- The purple arrow is `psi = f^-1 o h^-1`, the map from the learned variables back to the true ones (`U = psi(Z)`). It is unknown; the whole question is what `psi` can look like. If the model is identified, `psi` only renames and rescales the variables (the `phi` of slide 25).
- Notation remark: the paper writes `V` for our `U`.

### Slide 23: General assumptions, recall from the common setup (1 min)
- A recall, not a new explanation: four assumptions inherited from the shared setup. Go through them fast.
- Latent causal structure: the latents follow a DAG and the distribution factorizes along it.
- Multi-environment data: unpaired, labels known, targets unknown.
- Mechanism invariance: the mixing and all non-intervened mechanisms are shared.
- Atomic interventions: one target per intervention.

### Slide 24: General assumptions, additional assumptions (1.5 min)
- What this paper assumes on top of the common setup.
- Mixing: any diffeomorphism onto its image, no parametric form. Say aloud that the causal mechanisms are unrestricted too (arbitrary functions of parents and independent noise): nothing in the model is parametric.
- Perfect interventions: the target loses its incoming edges.
- The number of latents is known.
- Standard faithfulness, as in the common setup.
- Objective, say it aloud: strong identifiability guarantees without parametric restrictions on mixing or mechanisms.
- The theorem-specific assumptions A1-A4 come later, with the theorems.

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

### Slide 28: Proof strategy, eliminating cross-dependencies (1.5 min)
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

### Slide 30: Completing the proof, assumptions used (1 min)
- Say that this is a sketch, and do not explain the remaining steps: only name the assumption each one uses.
- Upper-right entry: A1, A2, A3 (previous slide).
- Lower-left entry: A1 and A2, and here it matters that the intervention on the child is perfect. One sentence: this is the step that fails for soft interventions, which is what Causal Disentanglement addresses. Do not claim perfect interventions are necessary in general.
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

### Slide 32: Causal influence, a simple example (1.5 min)
- Motivation, say it aloud: names and scales of the latents are arbitrary, so numerical effects cannot be read off. Which causal quantities survive?
- A concrete case: `U2 = 2 U1 + noise`. Left: samples from the original model, strong positive dependence.
- Right: the edge is removed by feeding `U2` an independent copy of `U1`. The marginals of `U1` and `U2` are the same as before, but the two are now independent: the cloud is no longer tilted.
- Same axes in both plots; the samples are synthetic (fixed random seed).
- The causal influence is the KL divergence between the two joint distributions: how much the joint distribution changes when this causal connection is removed. No derivation.

### Slide 33: Causal influence, definition (1.5 min, two clicks)
- The same construction in general. Left: the arrow from `Ui` to `Uj` is removed by feeding `Uj` an independent copy of `Ui`, drawn from its marginal.
- First formula: the new mechanism of `Uj`. Second: the causal influence, the KL divergence between the original distribution and the one with the arrow removed. It is zero when removing the arrow changes nothing, and grows with the strength of the arrow.
- Click: Theorem 4.2. The value is the same in every CRL-equivalent representation: unchanged under element-wise invertible rescaling, and it follows the variables under permutation. No proof.
- Conclusion, say it aloud: despite the unavoidable ambiguities, the learned graph keeps meaningful quantitative information.

### Slide 34: Ground truth, how the data are generated (1.5 min)
- Read the picture left to right: true latent graph, shared mixing `f`, observed dataset. Same layout as the candidate slides that follow, in the opposite direction.
- Latent model: two variables, `U1 -> U2`, linear Gaussian: `U1` is noise, `U2 = alpha U1 + noise`. The coefficient `alpha` is drawn away from zero, to stay away from unfaithful models.
- Three environments: observational; a perfect intervention on `U1`; a perfect intervention on `U2`. An intervention replaces the mechanism by Gaussian noise with shifted mean (plus or minus 2); for `U2` this removes the edge.
- Mixing: a small invertible MLP, three 2x2 weight matrices with an invertible nonlinearity, the same in all environments.
- This is repeated for 50 different ground truths (different `alpha` and mixing weights).
- What the learner sees: only the three datasets on the right, with their labels. Not the graph, not the targets, not `f`.

### Slides 35-38: the four candidate models (3 min in total)
- The slides carry no text: everything here is said aloud. The contribution of the paper is theoretical; the learning method is a proof of concept. Of the two proposals (autoencoder with invariance constraints, maximum likelihood) the experiments use the second.
- Same layout on all four slides. Left: the three datasets, always the same (`e0` observational, `e1` and `e2` interventional). Centre: one normalizing flow `h_k`, shared by the three environments. Right: the latent graph the candidate assumes in each environment; the red node is the variable it treats as intervention target.
- Slide 35, candidate 1 (blue): correct graph, aligned targets. In `e1` the target is the root `Z1`, so the edge stays; in `e2` the target is `Z2` and, the intervention being perfect, its incoming edge is removed.
- Slide 36, candidate 2 (orange): correct graph, targets swapped. `e1` is explained as an intervention on `Z2`, `e2` as one on `Z1`.
- Slide 37, candidate 3 (red): wrong graph, aligned targets. In the paper the wrong graph means the two learned variables are assumed independent (no edge), not a reversed edge.
- Slide 38, candidate 4 (purple): wrong graph, targets swapped.
- For each candidate, graph and targets are fixed; the flow and the mechanisms are learned. The mixing and the non-intervened mechanisms are shared across environments. No architecture details.

### Slide 39: Maximum likelihood and model selection (1 min)
- The same three datasets go to all four candidates. Each has its own flow and its own three graphs (the miniatures: columns are `e0`, `e1`, `e2`).
- Each candidate is trained by maximum likelihood and gets a validation log-likelihood.
- Say aloud (the formula is no longer on the slide): by change of variables, the log-likelihood of `x` is the log-density of the latent `h_k(x)` under the candidate's causal model plus the log-determinant of the Jacobian of the flow.
- The candidate with the highest one is selected. Do not say the correct model always wins: it does in most runs, not in all.
- Limitation, say it aloud: this is an exhaustive search over graphs and target assignments; it does not scale.

### Slide 40: Experimental results (1.5 min)
- The four miniatures on top are the colour legend of the plot.
- Left panel: MCC, recovery of the true latents; close to one only for the correct model (blue).
- Right panel: difference in validation log-likelihood between the correct model and each misspecified one; mostly positive, so the correct model is generally the best.
- Transition, say it aloud: "Despite these strong theoretical guarantees, the assumptions on interventions remain restrictive, and the learning approach is not scalable."

## Section 6: limitations and motivation (about 3.5 min)

### Slide 42: Limitations (2 min)
- Perfect interventions only, while CRISPR activation and drugs are soft.
- Known number of latents.
- Paired interventions for more than two latents.
- No scalable algorithm, and only toy experiments.
- The authors themselves name soft interventions as future work.

### Slide 43: Side by side (1.5 min)
- Read the red cells only: polynomial mixing, soft interventions, number of latents learned, a VAE-based algorithm.
- Same in both: nonparametric mechanisms, unknown targets, unpaired data.
- The last row shows the difference in scale.
- Hand-over to Joan (the motivation slide was removed, say it here): Causal Disentanglement restricts the mixing and accepts that single latents are not recovered one by one; in exchange it handles soft interventions, an unknown number of latents, one intervention per node, and comes with a method for real data. If interventions only change mechanisms instead of replacing them, what can still be identified, and how do we learn it?
