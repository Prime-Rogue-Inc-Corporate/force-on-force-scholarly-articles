# Recommendations

The reviewer adds entries. The model judge answers under each on `Model judge:` lines and sets `Status`.
Format and rules are in `INSTRUCTIONS.md`. Newest entries go at the bottom; numbers are never reused.

## R-001: Bear season starts in May, not April

- Parameter or mechanism: active bear season in `wildlife` (module 0.1.2.6.1; the site describes
  `wildlife.bear_encounter_rate` as applying Apr–Nov, polar bears year-round)
- Model now: April–November, eight active months. Source line: module description, modeller estimate.
- Evidence: Herrero & Higgins (2003), *Ursus* 14(1):44–54, a census of all 42 serious or fatal
  bear-inflicted injuries in Alberta 1960–98, records injuries from May to November with a
  September peak and none at all in December–April inclusive (p. 47, Fig. 3 p. 50).
  Review: [reviews/herrero-2003-alberta-bear-injuries.md](reviews/herrero-2003-alberta-bear-injuries.md)
- Recommendation: narrow the black/grizzly season to May–November (seven months). Leave polar
  bears year-round; this paper covers neither polar bears nor the territories.
- Confidence: high for Alberta. A 39-year provincial census with zero April incidents is about as
  clean as this literature gets. Medium for the rest of the occupied area, since the paper covers
  one province and denning dates vary with latitude — April is likelier to be non-zero in southern
  BC and Ontario than in Alberta.
- Expected effect: bear exposure falls by about one-eighth. Given bears are 0.2–0.5% of US deaths,
  expect this to be noise in every scenario. It is a correctness fix, not a result-mover.
- Status: deferred
- Model judge: Deferred on 19 November 2026 at v0.1.3.9.2. That version only fills in potash site positions and imagery and
  changes no parameter. This entry gets a ruling at the next version that changes the model's rules (0.1.3.10).

## R-002: Raise the black/grizzly fatality share, and drop the armed-discount rationale

- Parameter or mechanism: `wildlife.bear_casualty_share`
- Model now: 0.02 – 0.05 – 0.1, "share of dangerous encounters that injure someone (armed troops
  usually shoot first); ~15% of attacks fatal (Wilder et al. 2017)". Source line: modeller
  estimate; Wilder et al. (2017).
- Evidence: Herrero & Higgins (2003) record 12 deaths among 42 serious or fatal injuries — 29% —
  with black bear incidents fatal in 42% of cases (5 of 12) and grizzly in 32% (7 of 22) (p. 47).
  More importantly, the armed-discount rationale is not supported by the one comparable exposure
  class the paper contains: people who had been hunting account for 50% of grizzly injuries on
  Alberta provincial lands (4 of 8) and 35% in British Columbia (17 of 49) (p. 52). Being armed
  did not make that group safer, and the model applies the discount to the outcome term while
  attractants and habitat time drive the rate.
  Review: [reviews/herrero-2003-alberta-bear-injuries.md](reviews/herrero-2003-alberta-bear-injuries.md)
- Recommendation: (a) use a fatality share of about 0.29 (range 0.25–0.42) for black and grizzly
  bears, keeping the Wilder figure for polar bears only; (b) either remove "armed troops usually
  shoot first" as the justification for the low end of `bear_casualty_share`, or widen the upper
  bound to 0.15 so the hunter evidence is inside the range. Also resolve an internal
  inconsistency: the site's 15%-fatal figure does not match its own actor datum
  `polar_bear_attacks` (20 deaths in 73 attacks, 27%). I have not read Wilder et al., so this is a
  query against the repository's numbers, not a finding about that paper.
- Confidence: medium. High on the Alberta fatality share as a count, low on transferring the
  hunter analogue to infantry, which no paper covers.
- Expected effect: bear casualties and wildlife deaths rise modestly in full annexation and the
  Alberta detachment; outcome shares should stay within noise. In the Arctic seizure, where total
  deaths are ~10, keep the polar-bear figures unchanged so this does not leak into the one
  scenario where wildlife moves the result.
- Status: deferred
- Model judge: Deferred on 19 November 2026 at v0.1.3.9.2. That version only fills in potash site positions and imagery and
  changes no parameter. This entry gets a ruling at the next version that changes the model's rules (0.1.3.10).

## R-003: Replace the low-confidence bear-attack datum, split grizzly from black, and make the
## exposure multiplier explicit

- Parameter or mechanism: actor datum `bear_attacks_north_america`; `wildlife.bear_encounter_rate`
- Model now: `bear_attacks_north_america` = "about 11 attacks a year; grizzly ~1.6 and black bear
  ~1.25 deaths a year in North America", source line "Secondary compilations (animal-world.com,
  petpedia) of published studies; low confidence". `wildlife.bear_encounter_rate` = 0.5 – 1.5 – 4
  dangerous encounters per 10,000 troops in bear country per active month, modeller estimate.
- Evidence: Herrero & Higgins (2003) is a peer-reviewed census that can replace the pet-trivia
  compilation for Canada: 42 serious or fatal injuries and 12 deaths in Alberta over 39 years
  (~1.1 injuries and ~0.31 deaths a year in one province), with a per-capita rate flat across four
  decades at 0.49–0.56 per million people per year (Table 4, p. 48; no trend, F = 0.13, P = 0.76,
  p. 47). The same paper shows grizzly and black bears differ in motivation (18% vs 58% predatory,
  p. 50), duration, lethality (p. 47) and range (Table 1, p. 45), and that no incident involved
  more than one bear (p. 49).
  Review: [reviews/herrero-2003-alberta-bear-injuries.md](reviews/herrero-2003-alberta-bear-injuries.md)
- Recommendation: (a) cite this paper in place of animal-world.com and petpedia for Canadian
  bear-attack frequency, and raise that datum's confidence from low to medium; (b) split the bear
  channel into grizzly and black with per-province range weights, since the model is already
  provincial and Alberta is its own scenario; (c) **keep `wildlife.bear_encounter_rate` as
  judgement and widen it.** The paper has no exposure denominator — no person-days in habitat —
  and explicitly declines to generalise beyond its own population and period (p. 46), so it cannot
  set a per-troop-month rate. What it can do is anchor the civilian baseline: the model's
  midpoints imply about 0.6 bear injuries per 10,000 troops per year against Alberta's observed
  0.04 per 10,000 people per year, i.e. an implicit assumption that troops are ~15× more exposed
  than the average Albertan. Make that multiplier an explicit, sampled parameter and report the
  implied injuries per 10,000 troops per year as an output, so it can be checked against this
  paper rather than buried in two parameters.
- Confidence: high on (a), medium on (b), high on (c) as a reporting change and low on any
  specific value for the multiplier — which is the point of the recommendation.
- Expected effect: (a) and (b) change sourcing and granularity, not results. (c) changes nothing
  by itself but makes the module falsifiable, and may show the current range is too narrow at the
  top once camp attractants are considered (see the attractant mechanism in the review, which I
  have not raised as its own entry because the module would need a camp-density input it does not
  have).
- Status: deferred
- Model judge: Deferred on 19 November 2026 at v0.1.3.9.2. That version only fills in potash site positions and imagery and
  changes no parameter. This entry gets a ruling at the next version that changes the model's rules (0.1.3.10).
