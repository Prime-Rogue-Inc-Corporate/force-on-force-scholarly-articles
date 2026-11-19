# Plan

## Status, 18 November 2026

Nothing in this file is a finding. No paper has been read, because there is none to read:

- `papers/inbox/` holds its own README and nothing else — no PDFs, no `links.md`.
- `papers/` is empty, `reviews/` holds only `.gitkeep`, `RECOMMENDATIONS.md` has no entries.

So there is no reading order to set. What follows is the priority rule papers will be read
under, the queue by topic, which of the seven topics have no paper (all seven), and what I
need from Kevin.

### What I read to write this

- `claude/force-on-force-architecture.md` (Project doc).
- https://forceonforce.si/sources.html — all 224 parameters, read in three passes.
- https://forceonforce.si/method.html **could not be read.** The site returned a client error
  on two attempts in this session. Nothing below reflects the limits that page states, which
  is a real gap: the Method page is where the model's own account of its faults lives. I will
  read it before the first review if it becomes reachable, and if it does not, Kevin can paste
  it into the chat.

I have not read `modules.html` yet; I will read it before the first recommendation, since a
recommendation needs the measured effect of a module to say which results should move.

## The priority rule

Rank each candidate paper by **leverage × weakness**:

- *Leverage*: how far the parameter or mechanism moves a terminal outcome
  (`attacker_withdrawal`, `defender_capitulation`, `annexation_consolidated`) rather than an
  intermediate quantity. Parameters inside the political layer dominate here, because in this
  model the war ends when US support falls or Canada capitulates, not when a line moves.
- *Weakness*: what the Sources page says the value rests on. A large majority of the 224
  parameters read "modeller estimate" or "modeller judgement". Two are worse than that and are
  worth naming: `political.casualty_reference` is "fitted by eye", and
  `political.capitulation_base_hazard` is "uncalibrated modeller estimate", which the
  architecture doc also calls the least-calibrated element in v1.

A paper that bears on a well-sourced parameter still gets read, but it goes behind one that
bears on a parameter holding up an outcome on judgement alone.

## Queue

### 0. First, verify the citations the model already leans on

These parameters cite real literature, but no PDF of any of it is in this repository, so the
citation is unchecked: the site's own source lines are paraphrases, and I cannot tell whether
the cited work supports the number, the mechanism, both or neither. Checking what is already
claimed is cheaper and more valuable than adding new sources, so it goes first:

- `kinetic.ratio_exponent` (1.5–2–2.5) — Biddle, *Military Power* (2004)
- `kinetic.attrition_base_rate`, `kinetic.defender_posture_mult`, `kinetic.defender_breakpoint`,
  `kinetic.air_superiority_mult` — Dupuy (1990), QJM factors, Bracken
- `occupation.density_high_resistance` (20/1,000) and `occupation.density_low_resistance`
  (2.5/1,000) — Quinlivan, *Parameters* (1995)
- `occupation.insurgency_median_months` (72–120–168) and
  `occupation.external_support_resistance_boost` — Connable & Libicki, RAND (2010); Byman et al. (2001)
- `occupation.civil_resistance_cost_mult` — Chenoweth & Stephan (2011)
- `political.mueller_slope` (0.06–0.1–0.15) — Mueller (1973); Gartner & Segura (1998)
- `oil.approval_per_10c` (0.003–0.006–0.009) — Harbridge, Krosnick & Wooldridge (2016)
- `oil.approval_cap` — Gupta, Pierdzioch & Tiwari (2025)

For each: does the cited work contain that number, at what page, under what case and period, and
does the model use it the way the author used it? A paraphrased source line is not a source.

### 1. Topic 1 — US casualty tolerance, and the support level at which the US gives up

Highest leverage of the seven. The whole withdrawal path runs through five parameters, three of
them pure judgement:

| Parameter | Model now | Source line |
|---|---|---|
| `political.mueller_slope` | 0.06 – 0.1 – 0.15 | Mueller (1973); Gartner & Segura (1998) |
| `political.casualty_reference` | 25 – 50 – 100 | fitted by eye to Iraq 2003–08 polling vs deaths |
| `political.withdrawal_threshold` | 0.15 – 0.22 – 0.3 | modeller estimate; Vietnam/Iraq support levels |
| `political.withdrawal_max_hazard` | 0.01 – 0.025 – 0.05 | modeller estimate; Iraq 2006–08 |
| `political.election_hazard_mult` | 3 – 5 – 8 | modeller estimate (1968, 2008) |

What would settle them: the casualty-tolerance literature proper, and specifically the dispute
between the log-casualties position and the success-expectation position, since the model's
support equation already contains both a Mueller log term and a Gelpi/Feaver/Reifler-style
success term and the weighting between them is the modeller's. Also wanted: anything that
estimates a *support level* at which withdrawal actually happens, rather than a slope — the
threshold is the parameter with the least literature behind it and the most effect, and I expect
this may end in "no good source; widen the range".

Transfer problem to state in every review here: this literature is about expeditionary wars
fought far from home against strangers. A war against Canada is contiguous, waged on a neighbour
with dense family, business and media ties into the United States. Casualty sensitivity could be
higher (a war most of the public never wanted, fought on the doorstep) or lower (home-hemisphere
framing, annexation as a stated objective). The sign is not obvious and no paper will settle it
directly. I will say so rather than smuggle a number across.

### 2. Topic 3 — Occupation force ratios, and how long pacifying a province takes

Second because the occupation layer drives both the deaths that feed topic 1 and the duration that
feeds everything. Parameters: the two Quinlivan densities above, plus
`occupation.hostile_kia_rate_ref` (9e-05 – 0.00013 – 0.00018, calibrated to Iraq 2003–11),
`occupation.resistance_relaxation` (0.05 – 0.08 – 0.12, modeller estimate, flagged "to calibrate
on Iraq data"), `occupation.shortfall_resistance_gain` (0.25 – 0.4 – 0.55, modeller estimate of the
Quinlivan mechanism), `occupation.resistance_ref` (0.6, modeller anchor), and
`occupation.local_force_substitution` (0 – 0.15 – 0.35).

Beyond values, two questions of form. First, the model makes resistance relax toward an
equilibrium that rises with control shortfall — a feedback loop asserted by the modeller from
Quinlivan's argument, not estimated. Whether any paper estimates that loop, in any case, matters
more than the coefficient. Second, pacification here is province-level; almost all of the
literature is country-level. Whether a per-province requirement is defensible, or whether
occupation requirements are non-additive across adjacent provinces, is a question I want a paper on.

Transfer: Iraq and Afghanistan supply nearly every number in this layer. A 40-million-person OECD
country with a professional army, no sectarian cleavage of the Iraqi kind, and an 8,900 km land
border to the occupier's own territory is not that case. `occupation.local_force_substitution`
is the parameter I trust least on transfer: a collaborator security force is a different
proposition in Canada than in post-Ba'athist Iraq.

### 3. Topic 2 — Canadian mobilization and Canadian will to continue

`mobilization.resolve_capitulation_damping` (0.1 – 0.25 – 0.4, modeller estimate, Finland model
cited in the DMP), `mobilization.cadre_resistance_coef` (0.02 – 0.04 – 0.06, modeller estimate
from Norway, the Baltics 1944–53, Ukraine TDF 2022), `mobilization.cadre_resistance_cap` (0.25
modeller cap), and the parameter they feed, `political.capitulation_base_hazard`
(0.002 – 0.008 – 0.02, uncalibrated).

This is where the model is weakest in its own estimation and where the literature is thinnest,
because capitulation by a consolidated democracy under invasion is a small-N problem. Wanted:
work on war termination and on surrender/resistance decisions by small states facing a much
larger neighbour; the Winter War, Norway 1940, the Baltic cases and Ukraine 2022 are the obvious
comparison set, and the model already gestures at them without a paper behind it. A levée-en-masse
literature on whether mobilization raises resolve or merely raises casualties would bear directly
on the sign of `resolve_capitulation_damping`.

### 4. Topic 4 — Allied response to an attack on a NATO member by a NATO member

Lower in the order than its importance, for a reason worth stating: 20-odd `nato_members.*`
parameters trace to a single deep-research report dated 12 Nov 2026, cited by section number
(s4.2, s7.2, s7.4, s7.6, s8). That is a single unrefereed source carrying an entire module, and it
is a structural weakness in the sourcing regardless of whether its numbers are right. But it is
also the topic least likely to be settled by scholarship: Article 5 contemplates an attack by a
third party, and intra-alliance aggression by the hegemon has no case base. My expectation is that
reviews here produce "no good source; keep as judgement, widen the range, and say so on the
Method page" more often than a value. Alliance-reliability and extended-deterrence-credibility
literature is the nearest thing worth reading, and I will be explicit that it is analogy, not
evidence.

### 5. Topic 5 — Weights turning lost potash and oil into lost US output and lost support

`potash.gdp_weight` (0.05 – 0.1 – 0.2) and `potash.political_weight` (0.03 – 0.06 – 0.1), both
modeller estimates resting on fertilizer being about 15% of farm costs and the 2021–22 price
episode; `oil.approval_per_10c` and `oil.approval_cap`, which do cite real work and belong in
queue 0; `economic.trade_va_share` (0.45 – 0.6 – 0.75, where the site itself notes the Canada–US
figure is not yet cited); `economic.supply_chain_amplifier` (1.2 – 1.6 – 2.2, modeller estimate);
`economic.oil_shock_gdp_per_mbd` (0.1 – 0.2 – 0.35, from the Hamilton literature by the modeller's
reading, with no paper behind it).

Wanted: oil-price-to-GDP pass-through estimates, gasoline-price-to-presidential-approval
estimates, and anything on input-price shocks reaching an electorate through a commodity most
voters never buy directly. The potash weights are the ones to doubt: a pass-through that reaches
voters through fertilizer, then farm costs, then food prices is three steps long and each step
is currently a single modeller coefficient.

### 6. Topic 6 — How fast lost potash can be replaced

`potash.substitution_max` (0.25 – 0.45 – 0.65), `potash.substitution_months` (6 – 12 – 18),
`potash.offshore_diversion` (0.1 – 0.25 – 0.4), `potash.occupied_mine_output` (0.3 – 0.6 – 0.8),
all modeller estimates. Tractable: this is a market-structure question with a real empirical base
in the 2021–22 Belarus sanctions episode and the Russian export disruption, which is a natural
experiment in exactly this substitution. Likely the topic where a paper changes a number most
cleanly. Mine ramp-up times and the capacity-expansion lead time are the quantities to find.

### 7. Topic 7 — Fertilizer shortfall to US farm yields, food prices and farm income

Planned work; no parameters on the site yet, so there is nothing to check a paper against. Reading
here should wait until the builder posts the mechanism, or be aimed at telling the builder what form
the mechanism should take before it is written. The second is probably more useful, and the
agronomic literature on yield response to potassium withdrawal over one to three seasons is where
I would start — the answer that soil potassium buffers a single missed season would change the
module's shape, not just its coefficients.

## Coverage: all seven topics have no paper

| Topic | Papers in repo | Present basis |
|---|---|---|
| 1. US casualty tolerance, give-up level | 0 | Mueller/Gartner & Segura cited, uncheckable; threshold is judgement |
| 2. Canadian mobilization and will | 0 | modeller estimate; historical cases named, none cited |
| 3. Occupation ratios, pacification time | 0 | Quinlivan and RAND cited, uncheckable; feedback loop asserted |
| 4. NATO response to intra-alliance attack | 0 | one deep-research report, 12 Nov 2026 |
| 5. Potash and oil weights | 0 | modeller estimates; two real citations, uncheckable |
| 6. Potash replacement speed | 0 | modeller estimate |
| 7. Fertilizer to yields and food prices | 0 | not yet modelled |

## What the literature may treat as decisive that the model lacks

Hypotheses, to be tested against papers rather than asserted. Recording them now so I can check
each against what arrives:

- **Elite and military dissent.** Termination in this model runs through mass public support and a
  hazard rate. The war-termination literature tends to put elite splits, and in this case the
  lawfulness of the order, closer to the decision.
- **Domestic resistance inside the occupier.** No mechanism for US-side refusal, non-compliance or
  unrest, and a war on Canada is the case where that is most plausible.
- **Refugee flows and the border as a civilian space.** Absent entirely.
- **Financial and currency channels.** The economic layer is trade, energy and sanctions. No
  market, debt or dollar channel, and that may be the fastest-moving cost in a real case.
- **Cross-border social ties** as a damper on both public support and occupation effectiveness.
- **Information and media environment**, which much of the casualty-tolerance literature treats as
  the mechanism rather than a context.

## What I need from Kevin

1. **Papers.** The inbox is empty. Nothing can be reviewed until PDFs land in `papers/inbox/`,
   with their Google Scholar links in `papers/inbox/links.md` or pasted in the chat. If you want
   the queue above followed, queue 0 and topic 1 are where PDFs pay back most.
2. **`method.html` is unreadable from here.** Two fetches failed with a client error. Paste the
   page, or point me at its source in the front-end repo.
3. **Repository access.** Attaching the repository with push access was refused by my session's
   permission classifier, and writing through the GitHub API returned 403 (not accessible to the
   integration). I can read the repository but not commit to it. Before the first review we also
   need a route for me to read a PDF's bytes — attaching the repo, or you uploading PDFs into the
   chat. I will not review from an abstract.
4. **The model's code repository name**, when the builder puts it on GitHub, so that reviews can
   check the implemented form of a mechanism and not just the site's description of it.
