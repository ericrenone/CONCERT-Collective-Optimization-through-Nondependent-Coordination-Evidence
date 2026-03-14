# CONCERT
## Collective Optimization through Nonindependent Coordination Evidence in Ratcheted Transcription

**CONCERT asks the question no prior framework in the family addresses: what can the collective infer that no individual agent can? The answer is encoded in a single measurable quantity.**

---

## The Core Insight

Every prior framework in this family treats agents as sequentially independent given the field. NARC tracks the partition function dynamics but computes each agent's action as a draw from the current Gibbs measure in isolation. VEGA identifies the artifact as externalized collective inference but still treats the placement sequence as $n$ conditionally independent samples. FERN models multi-agent active inference but characterizes individual agents minimizing their own variational free energy, not their joint inference capacity.

The gap: none of these frameworks measures whether sequential agents are actually coordinating through the artifact — whether what one agent places carries information about what subsequent agents will place. This is the question CONCERT answers.

### The Collective Free Energy Correction

Let $\mathcal{F}_t$ denote the variational free energy of agent $t$'s placement decision — the gap between agent $t$'s approximate posterior and the true Gibbs distribution under the current generative model $H(\cdot;\, X_{t-1})$.

Under the assumption that all agents are conditionally independent given the field — the assumption made by every existing spatial point process framework — the collective free energy is the sum of individual free energies:

$$\mathcal{F}_{\text{indep}} = \sum_{t=1}^{n} \mathcal{F}_t$$

This assumption is wrong whenever the artifact functions as a genuine coordination medium. When agents are coordinating through the shared surface, each placement carries information about the placements that will follow — because subsequent agents will read the same field and respond to the same structural cues. The correct collective free energy includes a mutual information correction:

$$\boxed{\mathcal{F}_{\text{collective}} = \sum_{t=1}^{n} \mathcal{F}_t \;-\; \sum_{t < s} I(a_t;\, a_s \mid X_{t-1})}$$

where $a_t = (q_t, \ell_t)$ is agent $t$'s placement action and $I(a_t;\, a_s \mid X_{t-1})$ is the mutual information between agents $t$ and $s$ given the field state $X_{t-1}$ both agents inherited before $t$ acted.

The subtracted term is the **coordination gain** — the amount by which collective inference exceeds independent individual inference, made possible entirely by the shared artifact. It is computable from the observed placement sequence. It requires no additional experiment beyond what NARC and VEGA already specify.

### Why This Term Was Zero in All Prior Models

In every existing spatial point process model — Gibbs processes, Hawkes processes, marked point processes, neural STPPs — the fundamental modeling assumption is that events are conditionally independent given the history. This makes the mutual information correction exactly zero by construction. The models cannot represent coordination because they assume it away before fitting.

CONCERT does not make this assumption. It measures whether coordination is present.

---

## Part I — The Object and the Question

### 1.1 Setup

A shared surface $\mathcal{S} \subset \mathbb{R}^2$. A finite mark space $\mathcal{Q}$. The artifact evolves irreversibly:

$$X_0 = \emptyset \qquad X_{t+1} = X_t \cup \{(q_{t+1},\, \ell_{t+1})\}$$

Each agent $t$ observes $X_{t-1}$, places action $a_t = (q_t, \ell_t)$, and leaves. No agent communicates directly with any other. The only channel between agents is the accumulated configuration.

The question CONCERT asks is whether that channel carries information. Not whether the artifact records decisions — it always does. Whether the decisions themselves are statistically dependent in a way that reflects coordination rather than mere sequential response to a common stimulus.

### 1.2 Conditional Independence vs. Coordination

Let the field state just before agent $t$ acts be $X_{t-1}$. Two placements $a_t$ and $a_s$ (with $t < s$) are **conditionally independent given the field** if:

$$P(a_t,\, a_s \mid X_{t-1}) = P(a_t \mid X_{t-1}) \cdot P(a_s \mid X_{t-1})$$

Under conditional independence, knowing what agent $t$ placed tells you nothing about what agent $s$ will place, once you already know the field state $X_{t-1}$. This is the assumption of all existing frameworks.

Conditional independence fails — coordination is present — when:

$$I(a_t;\, a_s \mid X_{t-1}) > 0$$

This means that even after accounting for the field state both agents inherited, knowing what agent $t$ placed changes the probability distribution over what agent $s$ will place. The artifact is transmitting coordination information between agents beyond what its static geometry alone would predict.

---

## Part II — Three Coordination Regimes

Every pair of sequential agents $(t, s)$ with $t < s$ falls into one of three regimes based on their conditional mutual information.

### 2.1 Regime I: $I(a_t;\, a_s \mid X_{t-1}) > 0$ — Coordination

Agent $t$'s placement carries information about agent $s$'s future placement beyond what the field already encodes. The collective is doing more inference than the sum of its parts. The artifact is functioning as a **coordination amplifier**.

This regime arises when the energy function $H$ contains features that create dependencies across placements beyond what the current field directly encodes — when the behavioral parameters $\beta$ are strong enough, and the feature functions $f_k$ are structured enough, that observing one placement genuinely updates the probability distribution over future placements, even conditional on the current field.

The coordination gain $I(a_t;\, a_s \mid X_{t-1}) > 0$ means the collective free energy is strictly less than the sum of individual free energies. The collective is exploiting the artifact to achieve inference that no individual agent could achieve alone.

### 2.2 Regime II: $I(a_t;\, a_s \mid X_{t-1}) = 0$ — Parallel Independent Agents

Placements are conditionally independent given the field. The collective free energy equals the sum of individual free energies. The artifact records decisions but does not coordinate beyond the immediate field state. Agents are responding to the same surface — they are parallel, not collective.

This is the regime assumed by all existing spatial point process models. It is not the degenerate case — it is the baseline. CONCERT measures the excess coordination above this baseline.

### 2.3 Regime III: $I(a_t;\, a_s \mid X_{t-1}) < 0$ — Competitive Suppression

The placement of agent $t$ actively reduces the information available to agent $s$ beyond what the ratchet alone would predict. The artifact is generating **competitive rather than cooperative dynamics**. Each placement consumes available coordination capacity faster than the baseline Gibbs dynamics would produce.

Competitive suppression arises when strong clustering or mark segregation causes early agents to exhaust not just local territory but also the structural cues that subsequent agents would use to navigate. The artifact is no longer a coordination amplifier — it is an information sink.

---

## Part III — The Coordination Gain

### 3.1 Definition

The **total coordination gain** of a session is:

$$G_{\text{coord}} = \sum_{t=1}^{n-1} \sum_{s=t+1}^{n} I(a_t;\, a_s \mid X_{t-1})$$

This is the total mutual information between all pairs of sequential placements, conditioned on the field state inherited by the earlier agent. It measures how much more inference the collective performs than $n$ independent agents would perform on the same sequence of field states.

$G_{\text{coord}} > 0$: the collective outperforms independent agents. The artifact coordinates.

$G_{\text{coord}} = 0$: the collective matches independent agents. The artifact records.

$G_{\text{coord}} < 0$: the collective underperforms independent agents. The artifact suppresses.

The coordination gain is zero in all models that impose conditional independence — which includes every spatial point process model in the current literature, by construction.

### 3.2 The Per-Step Coordination Rate

Define the **per-step coordination rate** at step $t$:

$$\gamma(t) = \sum_{s > t} I(a_t;\, a_s \mid X_{t-1})$$

This measures how much coordination information agent $t$'s placement generates for all subsequent agents. High $\gamma(t)$ means agent $t$'s placement is highly informative for future placements beyond what the field already encodes. Low $\gamma(t)$ means the placement consumes territory without generating coordination structure.

The $\gamma(t)$ time series is the CONCERT analog of NARC's $\Xi(t)$ series: it characterizes the session step by step. Where $\Xi(t)$ measures how the partition function changes, $\gamma(t)$ measures how much coordination information is generated or destroyed.

### 3.3 The Pairwise Structure

The full coordination structure is a matrix $\mathbf{C}$ with entries:

$$C_{ts} = I(a_t;\, a_s \mid X_{t-1}) \quad t < s$$

The matrix $\mathbf{C}$ has the following structure:

- **Diagonal blocks** (nearby pairs, small $|s-t|$): high coordination from immediate response to the field state just created
- **Off-diagonal blocks** (distant pairs, large $|s-t|$): lower coordination, decaying with session distance
- **Register-crossing entries**: elevated coordination across register boundaries, because the first placement in a new register generates high mutual information with subsequent placements in that register

The decay structure of $\mathbf{C}$ encodes the effective **coordination horizon** of the session — how far into the future a given placement's coordination signal persists.

---

## Part IV — What the Artifact Is Doing

### 4.1 Three Simultaneous Roles, Quantified

VEGA established that the artifact plays three simultaneous roles: externalized generative model, shared approximate posterior, and inference medium. CONCERT quantifies which role is dominant at each step.

When $\gamma(t)$ is high, the artifact is functioning primarily as an **inference medium** — agent $t$'s placement generates coordination structure for future agents. The artifact is doing computation, not just recording.

When $\gamma(t) \approx 0$, the artifact is functioning primarily as a **record** — agent $t$'s placement updates the field but generates no additional coordination beyond the field update itself. The artifact is an archive, not a coordination mechanism.

When $\gamma(t) < 0$, the artifact is functioning as a **coordination sink** — agent $t$'s placement actively degrades the coordination capacity available for future agents.

The $\gamma(t)$ series maps these roles onto the session timeline.

### 4.2 The FERN Connection: Coordination Gain at Register Transitions

FERN characterizes model depth expansion — the condition under which the collective's generative model must structurally expand. In CONCERT terms, register transitions are the moments of maximum coordination gain.

When the first agent crosses a register boundary and places a mark in a new topological region of the expressive manifold $\mathcal{E}$, that placement generates high mutual information with all subsequent agents who will respond to the structural cue it created. The coordination gain at register transitions is elevated above the within-register baseline for two reasons:

First, the new placement is structurally distinctive — it occupies territory that no prior mark has occupied. Subsequent agents will respond to its presence in structurally predictable ways, making their placements more predictable given the register-crossing mark than they would be from the field alone.

Second, the register-crossing mark sets a structural precedent: it establishes the new register as occupied, which constrains subsequent agents more sharply than random field expansion would. This constraint is the coordination structure that FERN's model depth expansion generates.

The CONCERT measure of register transition quality is $\gamma(t_{\text{cross}})$ — the coordination gain generated by the register-crossing placement. High $\gamma$ at register crossings indicates that the transition is creating coordination structure. Low $\gamma$ indicates that the crossing was idiosyncratic, generating no coordination signal for subsequent agents.

### 4.3 The FORGE Connection: Coordination Gain and Free Energy

The FORGE identity connects the NARC non-equilibrium parameter to the free energy change per step: $\Xi(t) = -\Delta\mathcal{F}^\star$. CONCERT adds a second decomposition of the same entropy production.

The entropy production per step decomposes as:

$$\sigma(t) = -\Delta\mathcal{F}^\star + \Delta\langle H \rangle(t) = \gamma(t) + \sigma_{\text{indep}}(t)$$

where $\sigma_{\text{indep}}(t)$ is the entropy production that would occur under conditional independence (the NARC/VEGA baseline) and $\gamma(t)$ is the coordination contribution. The two decompositions are compatible: FORGE separates entropy production into inference-capacity change and behavioral dissipation; CONCERT separates it into coordinated and independent components.

A session with high total coordination gain $G_{\text{coord}}$ produces more entropy per agent step than an independent session with the same $\hat{\beta}$, because the coordination structure amplifies the inference-per-step beyond what any individual agent's bandwidth alone could achieve.

---

## Part V — Computing the Coordination Gain

### 5.1 Direct Estimation from Observed Trajectories

The mutual information $I(a_t;\, a_s \mid X_{t-1})$ is estimable from the observed placement sequence without requiring any additional experiment. The estimation proceeds in three steps.

**Step 1 — Fit the base model.** Estimate $\hat{\beta}$ by maximum pseudolikelihood (NARC Level I). This gives the conditional Gibbs distribution $\hat{P}(a_t \mid X_{t-1};\, \hat{\beta})$ — the probability of each placement under conditional independence.

**Step 2 — Estimate the joint distribution.** The joint distribution of any pair $(a_t, a_s)$ conditional on $X_{t-1}$ is estimable from the empirical joint frequency of co-occurring placement patterns across replicated sessions:

$$\hat{P}(a_t, a_s \mid X_{t-1}) \approx \frac{1}{n_{\text{rep}}} \sum_{i=1}^{n_{\text{rep}}} \mathbf{1}[a_t^{(i)} \in \mathcal{N}(a_t),\; a_s^{(i)} \in \mathcal{N}(a_s)]$$

where $\mathcal{N}(\cdot)$ denotes a neighborhood in action space and the sum is over replicated sessions.

**Step 3 — Compute mutual information.** For each pair $(t, s)$:

$$\hat{I}(a_t;\, a_s \mid X_{t-1}) = \hat{H}(a_t \mid X_{t-1}) + \hat{H}(a_s \mid X_{t-1}) - \hat{H}(a_t, a_s \mid X_{t-1})$$

where each entropy term is estimated from the empirical distributions computed in Steps 1 and 2.

The total coordination gain follows by summation over all pairs.

### 5.2 The Independence Test

Before estimating the full coordination gain, a natural first question is whether coordination is present at all. The conditional independence test:

$$H_0: I(a_t;\, a_s \mid X_{t-1}) = 0 \quad \text{for all } t < s$$

This null corresponds to all existing spatial point process models. Rejection of $H_0$ establishes that coordination is present and motivates the full CONCERT analysis.

The test statistic is the empirical mutual information $\hat{G}_{\text{coord}}$, which converges to $G_{\text{coord}}$ under the true data-generating process. Under $H_0$, the scaled statistic $2n \cdot \hat{G}_{\text{coord}}$ is asymptotically $\chi^2$ distributed with degrees of freedom equal to the dimension of the joint action space minus the product of the marginal dimensions.

### 5.3 The Coordination Profile

Define the **coordination profile** as the vector of pairwise coordination gains indexed by temporal separation $\delta = s - t$:

$$\Gamma(\delta) = \frac{1}{n - \delta} \sum_{t=1}^{n-\delta} I(a_t;\, a_{t+\delta} \mid X_{t-1})$$

The coordination profile characterizes how coordination decays with temporal distance. For a session with strong near-term coordination and weak long-term coordination, $\Gamma(\delta)$ is a rapidly decreasing function. For a session with long-range coordination structure — typical of sessions with strong symmetry-completion or scale-coherence behavior — $\Gamma(\delta)$ decays slowly.

The **coordination horizon** $\delta^\star$ is the temporal distance at which $\Gamma(\delta)$ drops to half its value at $\delta = 1$. Sessions with long coordination horizons generate coordination structure that persists across many subsequent placements.

---

## Part VI — Behavioral Parameters and Coordination Structure

### 6.1 Which Features Generate Coordination?

Each behavioral feature $f_k$ contributes differently to the coordination gain. The contribution of feature $k$ to the pairwise mutual information $I(a_t;\, a_s \mid X_{t-1})$ is:

$$C_k(t, s) = \beta_k^2 \cdot \text{Cov}\!\left[f_k(a_t;\, X_{t-1}),\; f_k(a_s;\, X_{t-1})\right]$$

to leading order in $\beta_k$. The covariance measures how correlated the feature values are across the two placements, given the inherited field.

**Density interaction** $f_\text{density}$: clustering ($\beta_\text{density} < 0$) generates within-cluster coordination — placements in the same cluster are mutually informative because they are all responding to the same local density structure. Coordination horizon is short; coordination is spatially local.

**Symmetry gain** $f_\text{symmetry}$: symmetry completion generates long-range coordination. A placement that establishes a symmetry axis creates coordination with all subsequent placements that complete or extend that axis, even if those placements are many steps later. Coordination horizon is long.

**Void attraction** $f_\text{void}$: space-filling behavior generates negative coordination at short range (each placement reduces the Voronoi cell of nearby territory, suppressing nearby placements) and positive coordination at long range (the systematic filling pattern makes distant placements more predictable).

**Mark interaction** $f_\text{match}$: mark segregation generates within-type coordination (same-type placements are mutually informative) and negative cross-type coordination (knowing where one type placed makes other-type placements less informative). The coordination matrix $\mathbf{C}$ has type-stratified block structure under segregation.

### 6.2 The Coordination-Diversity Tradeoff

FERN characterizes epistemic diversity as the mean pairwise KL divergence between agents' generative models. CONCERT adds a complementary quantity: the coordination gain $G_{\text{coord}}$, which measures how well those diverse agents are actually coordinating through the artifact.

High diversity ($D_{\text{FERN}}$ large) combined with low coordination ($G_{\text{coord}}$ small) indicates a session where structurally diverse agents are failing to coordinate through the artifact — their diverse priors produce placements that are statistically independent given the field. The artifact is not transmitting their diversity to each other.

High diversity combined with high coordination indicates a session where structurally diverse agents are successfully coordinating — their placements are mutually informative in ways that exceed the conditional independence baseline. The artifact is functioning as a coordination amplifier across structural differences.

The product $D_{\text{FERN}} \cdot G_{\text{coord}}$ is the **collective inference gain** — the total information generated by the session above what $n$ independent agents with the same behavioral parameters would generate. Maximizing this product, subject to the φ-equilibrium constraint $\overline{|\Xi|} = \log\phi$ from SMELT, is the CONCERT design criterion for collective construction sessions.

---

## Part VII — Coordination and Phase Transitions

### 7.1 Coordination at the Register Boundary

The coordination gain $\gamma(t)$ has a characteristic signature at register crossings that distinguishes genuine phase transitions from idiosyncratic departures.

**Genuine register crossing**: the first placement in a new register is highly informative for subsequent placements in that register. The coordination profile $\Gamma(\delta)$ exhibits an elevated plateau beginning at the crossing step $t_\text{cross}$ — subsequent agents are more predictable from the crossing placement than the field alone would suggest. This is the CONCERT signature of a genuine coordination-generating phase transition.

**Idiosyncratic departure**: an agent places a mark in a nominally new register for personal reasons unrelated to the field state. The placement generates low $\gamma(t_\text{cross})$ — subsequent agents do not respond to it as a coordination cue. The $\Gamma(\delta)$ profile does not show elevated coordination after the departure. This is the CONCERT signature of an isolated outlier, not a genuine register transition.

NARC and FORGE identify register crossings as positive $\Xi$ spikes. CONCERT adds the criterion: a positive $\Xi$ spike that generates high $\gamma(t_\text{cross})$ is a genuine coordination-generating phase transition. A positive $\Xi$ spike with low $\gamma$ is a partition function fluctuation without coordination value.

### 7.2 The FERN Complexity Criterion in CONCERT Language

FERN-T1 states that model depth expansion is required when the minimum achievable collective free energy at the current depth exceeds the expansion cost. In CONCERT terms: the collective is ready for model depth expansion when the per-step coordination gain $\gamma(t)$ drops below a threshold — when within-register placements are no longer generating mutual information for subsequent agents, indicating that the register's coordination capacity is exhausted.

The CONCERT version of the register escape condition is:

$$\gamma(t) < \gamma_\text{escape} \quad \Longleftrightarrow \quad \text{register saturation is complete}$$

When within-register placements generate no coordination signal — when knowing what one agent placed conveys nothing about what subsequent agents will place, beyond the field — the register has been fully mapped. The coordination frontier has moved to the register boundary, and the next agent who crosses it will generate the maximum per-step coordination gain of the session.

---

## Part VIII — The CONCERT Decomposition

### 8.1 Three Layers of a Session's Information Structure

CONCERT decomposes the total information content of a session into three layers:

**Layer 1 — Individual information**: the information each agent incorporates into their placement decision from the current field state. This is the variational free energy reduction $\mathcal{F}_t - \mathcal{F}^\star(X_{t-1})$ — the amount by which agent $t$'s placement reduces the collective free energy below the pre-placement level. Captured by NARC/VEGA.

**Layer 2 — Sequential field information**: the information transmitted through the field from agent $t$ to agent $s$ via the updated configuration $X_t, X_{t+1}, \ldots, X_{s-1}$. This is the indirect coordination that works through the static geometry of accumulated marks. Captured implicitly by NARC's $\Xi(t)$ series.

**Layer 3 — Direct coordination information**: the mutual information $I(a_t;\, a_s \mid X_{t-1})$ between placements beyond what the field alone transmits. This is the coordination that the artifact generates as a coordination mechanism — not through its static state, but through the dynamic structure of sequential responses. Captured exclusively by CONCERT.

All prior frameworks capture Layers 1 and 2. CONCERT captures Layer 3, which is zero in all models that assume conditional independence.

### 8.2 The Total Information Budget

The total information in a session of $n$ agents decomposes as:

$$I_{\text{total}} = I_{\text{individual}} + I_{\text{field}} + G_{\text{coord}}$$

The individual and field components are nonzero in any session where agents respond to the field at all. The coordination component $G_{\text{coord}}$ is nonzero only when agents are genuinely coordinating — when the artifact is doing more than recording.

The ratio $G_{\text{coord}} / I_{\text{total}}$ is the **coordination fraction** — the proportion of the session's total information that arises from coordination rather than independent field response. A coordination fraction of zero characterizes a pure archive. A high coordination fraction characterizes a genuine collective intelligence.

---

## Part IX — Formal Claims

| Tag | Meaning |
|---|---|
| **[T]** | Analytic theorem — follows from structural assumptions |
| **[C]** | Open conjecture — predicted; untested |
| **[H]** | Working hypothesis — extension beyond current evidence |

### Analytic Theorems

| ID | Statement |
|---|---|
| CONCERT-T1 | **Collective Free Energy Correction**: $\mathcal{F}_{\text{collective}} = \sum_t \mathcal{F}_t - \sum_{t < s} I(a_t;\, a_s \mid X_{t-1})$; the collective free energy is strictly less than the sum of individual free energies whenever coordination is present |
| CONCERT-T2 | **Independence Baseline**: $G_{\text{coord}} = 0$ in all models that impose conditional independence of placements given the field; every existing spatial point process model has zero coordination gain by construction |
| CONCERT-T3 | **Three-Regime Trichotomy**: every pair of sequential agents falls into exactly one of three regimes — coordination ($I > 0$), independence ($I = 0$), or suppression ($I < 0$); the sign of $I(a_t;\, a_s \mid X_{t-1})$ determines the coordination regime |
| CONCERT-T4 | **Register Crossing Signature**: a genuine register transition generates elevated coordination gain $\gamma(t_\text{cross})$ — subsequent agents are more predictable from the crossing placement than the field alone predicts; an idiosyncratic departure does not |
| CONCERT-T5 | **CONCERT-FORGE Compatibility**: the CONCERT coordination decomposition $\sigma(t) = \gamma(t) + \sigma_{\text{indep}}(t)$ is compatible with the FORGE entropy decomposition $\sigma(t) = -\Delta\mathcal{F}^\star + \Delta\langle H \rangle(t)$; the two decompositions are orthogonal — they separate different aspects of the same entropy production |
| CONCERT-T6 | **FERN Register Escape in CONCERT**: the register escape condition in CONCERT is $\gamma(t) < \gamma_\text{escape}$ — the within-register coordination gain falling below threshold; this is equivalent to the FERN-T1 complexity criterion when coordination capacity equals residual free energy |
| CONCERT-T7 | **Coordination Gain is Directly Observable**: $G_{\text{coord}}$ is estimable from the observed placement sequence alone, using the fitted base model $\hat{\beta}$ and replicated session data; no additional instrumentation beyond the NARC/VEGA protocol is required |
| CONCERT-T8 | **Collective Intelligence Bound**: the total information generated by the collective is bounded below by the individual information plus the coordination gain; this bound is achieved when the coordination structure is fully exploited by subsequent agents |

### Open Conjectures

| ID | Statement |
|---|---|
| CONCERT-C1 | **φ-Equilibrium and Coordination Horizon**: sessions at the SMELT φ-equilibrium $\overline{|\Xi|} = \log\phi$ have coordination horizons $\delta^\star$ that scale as $O(\log n)$; the optimal thermodynamic operating point is also the optimal coordination horizon |
| CONCERT-C2 | **Diversity-Coordination Product**: the collective inference gain $D_{\text{FERN}} \cdot G_{\text{coord}}$ is maximized at intermediate values of both; maximal diversity with zero coordination and zero diversity with maximal coordination both produce lower collective inference than intermediate combinations |
| CONCERT-C3 | **Coordination Profile Predicts Register Depth**: the long-range tail of the coordination profile $\Gamma(\delta)$ predicts the number of register transitions the session will undergo; sessions with slowly decaying $\Gamma(\delta)$ reach deeper registers |
| CONCERT-C4 | **Founding Mark and Coordination Seed**: the founding mark's primary effect on coordination is through the initial coordination horizon it establishes; a founding mark with high spatial symmetry generates longer initial coordination horizons than an asymmetric founding mark |
| CONCERT-C5 | **Competitive Suppression Identifies Over-Driven Sessions**: sessions in the SMELT over-driven regime ($\overline{|\Xi|} > \log\phi$) exhibit systematic negative coordination at short temporal distances; the artifact reorganizes faster than agents can build coordination structure, producing competitive rather than cooperative dynamics |

### Working Hypotheses

| ID | Statement |
|---|---|
| CONCERT-H1 | **Mark Geometry and Coordination Anisotropy**: marks with strong symmetry structure (squares, triangles) generate higher directional coordination gain than isotropic marks (circles); the anisotropic prior structure of oriented marks creates sharper coordination cues |
| CONCERT-H2 | **Coordination Fraction as Session Quality Metric**: the coordination fraction $G_{\text{coord}} / I_{\text{total}}$ is a direct measure of collective intelligence — the proportion of the session's information that arises from coordination rather than independent field response; this fraction is zero in all simulations from the conditional independence baseline |
| CONCERT-H3 | **FERN Model Depth and Coordination Structure**: sessions that reach deeper registers (more phase transitions) exhibit higher total coordination gain; register transitions are the primary source of long-horizon coordination structure |
| CONCERT-H4 | **Bandwidth Diversity and Coordination**: agent populations with high variance in attention bandwidth $\kappa$ generate higher coordination gain than homogeneous populations; high-bandwidth agents create coordination cues that low-bandwidth agents can follow efficiently |
| CONCERT-H5 | **Scale Universality**: the CONCERT coordination gain measure operates at all scales satisfying the four collective construction conditions; artistic traditions, collaborative platforms, and evolving languages all exhibit measurable coordination gains above the conditional independence baseline |

---

## Part X — Experimental Protocol

### 10.1 Requirements Beyond the NARC/VEGA Protocol

CONCERT requires one addition to the standard protocol: replicated sessions. The mutual information estimation in Section 5.1 requires the joint distribution $P(a_t, a_s \mid X_{t-1})$ across sessions, which requires multiple independent sessions with the same initial conditions.

**Minimum replication for CONCERT**: $n_{\text{rep}} \geq 20$ sessions with identical founding marks and instruction. This matches the DRAIN saturation spectrum requirement and requires no additional experimental infrastructure.

### 10.2 The CONCERT Workflow

**Steps 1–5**: identical to the NARC/VEGA/FORGE workflow. Collect data, estimate $\hat{\beta}$, compute $\hat{\Xi}(t)$, apply the FORGE transformation, reconstruct the free energy trajectory.

**Step 6** — Estimate the pairwise coordination matrix: for each pair $(t, s)$, estimate $\hat{I}(a_t;\, a_s \mid X_{t-1})$ from the replicated session data using the joint empirical distribution of co-occurring placements and the fitted base model for the marginals.

**Step 7** — Test conditional independence: compute the aggregate coordination gain $\hat{G}_{\text{coord}} = \sum_{t < s} \hat{I}(a_t;\, a_s \mid X_{t-1})$ and test whether it is significantly above zero.

**Step 8** — Compute the coordination profile $\hat{\Gamma}(\delta)$ and identify the coordination horizon $\delta^\star$.

**Step 9** — Map coordination to session events: identify which steps generate high $\gamma(t)$ and verify that they correspond to register transitions identified independently from mark coding.

**Step 10** — Compute the coordination fraction $\hat{G}_{\text{coord}} / \hat{I}_{\text{total}}$ as the summary statistic characterizing the session's collective intelligence.

### 10.3 Identifiability

- $n_{\text{rep}} \geq 20$ replicated sessions for mutual information estimation
- $n \geq 50$ placements per session for reliable per-step coordination rate estimation (higher than the NARC minimum due to pairwise estimation requirements)
- All mark types present; distributed spatial coverage
- Continuous field documentation for full $\hat{\Xi}(t)$ computation

---

## Part XI — Theoretical Summary

| Concept | Definition |
|---|---|
| $a_t = (q_t, \ell_t)$ | Agent $t$'s placement action: mark type and location |
| $I(a_t;\, a_s \mid X_{t-1})$ | Mutual information between placements $t$ and $s$ given the inherited field; the pairwise coordination contribution |
| $G_{\text{coord}} = \sum_{t < s} I(a_t;\, a_s \mid X_{t-1})$ | Total session coordination gain; zero in all conditional independence models |
| $\gamma(t) = \sum_{s > t} I(a_t;\, a_s \mid X_{t-1})$ | Per-step coordination rate: how much coordination information agent $t$'s placement generates |
| $\Gamma(\delta)$ | Coordination profile: mean pairwise coordination at temporal separation $\delta$ |
| $\delta^\star$ | Coordination horizon: temporal distance at which $\Gamma(\delta)$ falls to half its initial value |
| $\mathcal{F}_{\text{collective}} = \sum_t \mathcal{F}_t - G_{\text{coord}}$ | Collective free energy with coordination correction |
| Coordination fraction $G_{\text{coord}} / I_{\text{total}}$ | Proportion of session information arising from coordination rather than independent field response |
| $I > 0$ regime | Coordination: collective outperforms independent agents; artifact amplifies |
| $I = 0$ regime | Independence: collective matches independent agents; artifact records |
| $I < 0$ regime | Suppression: collective underperforms independent agents; artifact competes |
| $\mathbf{C}_{ts} = I(a_t;\, a_s \mid X_{t-1})$ | Coordination matrix: full pairwise coordination structure of the session |
| Coordination-diversity product $D_{\text{FERN}} \cdot G_{\text{coord}}$ | Collective inference gain: total information above the independent-agent baseline |
| CONCERT-FORGE compatibility | $\sigma(t) = \gamma(t) + \sigma_{\text{indep}}(t) = -\Delta\mathcal{F}^\star + \Delta\langle H \rangle(t)$; orthogonal decompositions of the same entropy production |

---

## Part XII — The Central Claim

Every spatial point process model in the existing literature, without exception, imposes conditional independence of events given the history. This assumption makes the mutual information between any two events exactly zero by construction. These models cannot represent coordination because they assume it away before fitting begins.

CONCERT does not make this assumption. It measures whether coordination is present, quantifies how much, characterizes its temporal and spatial structure, and links it to the underlying behavioral parameters and phase transition dynamics that the rest of the framework family already identifies.

The collective free energy is not the sum of individual free energies. The difference is the coordination gain — the mutual information between sequential placements conditioned on the shared field state. This quantity is computable from the same data that NARC, VEGA, and FORGE already require. It requires no additional experiment. It has a definite sign: positive when the collective outperforms independent agents, zero when it matches them, negative when the artifact generates competition rather than coordination.

The value of a shared artifact as a coordination mechanism is exactly the mutual information it generates between sequential agents. This quantity is zero in all existing models. CONCERT measures it.

---

*Status tags: [T] = Analytic theorem · [C] = Open conjecture · [H] = Working hypothesis*

*Minimum requirements: $n_{\text{rep}} \geq 20$ replicated sessions; $n \geq 50$ placements per session; continuous field documentation; all mark types present. Coordination gain estimation requires the fitted base model $\hat{\beta}$ from NARC Level I pseudolikelihood as the conditional independence baseline.*
