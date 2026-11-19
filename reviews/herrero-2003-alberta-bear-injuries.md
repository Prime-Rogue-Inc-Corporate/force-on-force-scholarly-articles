# Herrero & Higgins (2003), Human injuries inflicted by bears in Alberta: 1960–98
*Ursus* 14(1):44–54. Peer-reviewed (journal of the International Association for Bear Research
and Management). PDF: papers/herrero-2003-alberta-bear-injuries.pdf

**Identity note.** This PDF arrived named as Herrero, Higgins, Cardoza, Hajduk & Smith (2011),
"Fatal attacks by American black bear on people: 1900–2009", *Journal of Wildlife Management*
75(3):596–603, from an academia.edu download link. The file is not that paper. All eleven pages
are the 2003 *Ursus* article above (page footers read `Ursus 14(1):44-54 (2003)` throughout). The
2011 paper is still wanted and is listed as such in `BIBLIOGRAPHY.md`. Reviewed under its real
identity.

## What it found

All known serious or fatal bear-inflicted injuries in Alberta, 1960–98: 42 injuries-plus-deaths
from 34 incidents, 29 (69%) by grizzly and 13 (31%) by black bear, with 12 fatalities (p. 44,
Table 3 p. 47). Against estimated provincial populations of about 1,000–1,075 grizzly and
38,160–39,192 black bears (Table 1, p. 45), so grizzlies inflicted more than twice the injuries
from about 1/35th the population.

Findings that bear on a model:

- **Rate is flat per capita.** Absolute counts rose each decade (7, 10, 12, 13) but the rate per
  million people per year did not: 0.49, 0.56, 0.50, 0.53 for the 1960s through 1990s
  (Table 4, p. 48), with no trend (F = 0.13, P = 0.76, p. 47). The rise tracks Alberta's
  population.
- **Season.** Injuries ran May–November, peaking in September, with a secondary August peak
  (p. 47, Fig. 3 p. 50). Zero in December–April.
- **Time of day.** 73% of grizzly incidents (16 of 22) and 73% of black bear incidents (8 of 11)
  with a known time happened between 06:00 and 18:00 (p. 47). Only three grizzly incidents
  occurred 00:00–06:00, all associated with food or garbage attractants (p. 51).
- **Mechanism differs by species.** 18% (4 of 22) of grizzly incidents were predatory against 58%
  (7 of 12) of black bear incidents (p. 50). 64% (14 of 22) of grizzly incidents were classified
  as "startled", and in all 11 of those with a known encounter distance it was under 50 m (p. 50).
  Grizzly attacks were mostly short (7 of 12 known durations under two minutes); black bear
  attacks mostly long, 10–30 minutes (pp. 50, 52).
- **Lethality.** 42% of black bear incidents (5 of 12) were fatal against 32% of grizzly (7 of 22)
  (p. 47). Across all 42 serious-or-fatal injuries, 12 were deaths — 29%.
- **Attractants.** 36% (8 of 22) of grizzly incidents involved food or garbage near the site, a
  bear with a feeding history, or a bear searching for it (p. 50). Every grizzly injury that
  happened in camp was associated with food or garbage (p. 52). Half of all serious or fatal
  grizzly incidents in the national parks had some food or garbage involvement (p. 53).
- **Armed people in habitat.** 50% (4 of 8) of grizzly injuries on Alberta provincial lands
  involved someone who had been hunting immediately before the attack; the British Columbia
  figure was 35% (17 of 49) (p. 52). No injuries to hunters by black bears were recorded in
  either province (p. 52).
- **One bear per incident.** None of the 34 incidents involved more than one bear (p. 49).
- **Party size.** Injuries fell overwhelmingly on parties of one to three; all eleven black bear
  incidents with a known party size involved one or two people (p. 48). The authors flag that
  they could not find the frequency of different party sizes among people in bear habitat, so
  "inferences regarding differential risk by party size are weak" (p. 52).

## Under what conditions (cases, period, method, sample)

Province of Alberta, 1960–98, provincial lands plus Banff, Jasper, Waterton Lakes and Wood
Buffalo national parks. Case-series census, not a sample: the authors state they believe the data
cover all such incidents in the period and therefore did not use significance tests on counts,
and warn against generalising beyond the population and period studied (p. 46). "Serious" is
defined as requiring 24 hours or more of hospitalisation (p. 46); minor injuries were excluded as
inconsistently recorded. Victims were recreationists, hunters, campers and workers (Table 6,
p. 50). Human-population denominators come from Statistics Canada; there is **no exposure
denominator** — no person-days or person-hours in bear habitat anywhere in the paper. The authors
themselves note injury numbers are best predicted by people–bear interaction rates (citing
Martinka 1982, p. 51), a quantity they do not measure.

## Key passages

> "There were no serious injuries or fatalities recorded from December to April, inclusive" (p. 47)

Quoting is kept to this one passage deliberately: the repository is public, and the rest of what
this paper contributes is counts and rates, which are reported above as figures with their page
and table numbers.

## What it means for the model

Module 0.1.2.6.1 (Bears and wildlife), `wildlife.*`. Current values copied from
https://forceonforce.si/sources.html:

| Parameter | Model now | Source line on the site | This paper |
|---|---|---|---|
| `wildlife.bear_encounter_rate` | 0.5 – 1.5 – 4 dangerous encounters per 10,000 troops in bear country per active month (Apr–Nov) | Modeller estimate | Does not reach it. No exposure denominator exists in the paper, so no per-troop-month rate can be derived |
| `wildlife.bear_casualty_share` | 0.02 – 0.05 – 0.1 of encounters injure someone; "armed troops usually shoot first"; ~15% of attacks fatal (Wilder) | Modeller estimate; Wilder et al. (2017) | Contradicts the armed-discount rationale. Supports a higher fatality share for black/grizzly: 29% of serious-or-fatal injuries were deaths (p. 47) |
| Active bear season, Apr–Nov | Apr–Nov | Module description | Contradicts April. Zero injuries Dec–April inclusive (p. 47); season ran May–November |
| Actor datum `bear_attacks_north_america` | ~11 attacks a year; grizzly ~1.6 and black ~1.25 deaths a year in North America; **low confidence**, sourced to animal-world.com and petpedia | Secondary compilations | Replaces it for Canada with peer-reviewed counts: 42 serious-or-fatal injuries and 12 deaths in Alberta over 39 years (~1.1 injuries and ~0.31 deaths a year in one province) |
| Single bear channel plus polar bears | one `bear_encounter_rate` | Modeller estimate | Supports splitting grizzly from black: different motivation mix, duration, lethality and range (pp. 45, 50, 52) |
| Wildlife deaths count toward US deaths for opinion | "a death is a death" | Module design | Does not reach it |

Two further observations, both about the model rather than the paper:

1. **An internal arithmetic check.** The site's `wildlife.bear_casualty_share` line says about 15%
   of attacks are fatal, citing Wilder et al. (2017); the actor-data entry `polar_bear_attacks`
   on the same page records 73 attacks with 20 deaths and 63 injuries, which is 27% of attacks
   fatal. One of the two is wrong. I have not read Wilder, so this is a query against the
   repository's own numbers, not a claim about that paper.
2. **Order of magnitude.** The model's midpoints imply roughly 0.6 bear injuries per 10,000 troops
   per year in bear country (1.5 encounters × 0.05 × 8 active months). Alberta's observed civilian
   figure is about 0.04 per 10,000 people per year (Table 4, p. 48). The model therefore assumes
   troops are roughly 15× more exposed than the average Albertan. That is not implausible —
   Alberta's population is mostly urban and spends little time in habitat, while troops in bear
   country are in it continuously — but the multiplier is currently implicit. It should be stated
   as an exposure assumption and reported as an output, so it can be checked against this paper.

## Does it transfer to a US–Canada war?

Better than most of this literature, and worse than it first looks.

**Transfers well.** The geography is the model's own: Alberta, the province in its own detachment
scenario, with provincial and national-park lands distinguished. Season, species mix, lethality
split, the single-bear constraint and the attractant mechanism are all properties of bears and
terrain, not of the people involved, and none depend on the exposure problem below.

**Does not transfer.** The rate level. Victims here are hikers, campers, hunters and workers in a
peacetime province; the denominator is the whole provincial population, overwhelmingly urban. An
occupying force is a different exposure class in every respect — continuously in habitat, armed,
in larger groups, generating concentrated waste at field camps. The paper gives no exposure
denominator and explicitly declines to generalise beyond its own population and period (p. 46),
so it cannot be used to set `wildlife.bear_encounter_rate`. It can only bound the civilian
baseline the model multiplies up from.

**Cuts against the model's assumption.** The module's rationale is that armed troops shoot first,
so casualties are rare. Hunters are the nearest civilian analogue — armed, in small groups, in
bear country, sometimes with carcasses — and they account for half of grizzly injuries on Alberta
provincial lands and 35% in British Columbia (p. 52). Being armed did not make that group safe.
It plausibly made it *more* exposed, by putting it in habitat with a kill. Whatever being armed
does to the outcome of an encounter, it does not lower the encounter rate, and the model applies
the discount to the outcome term only.

**My inference, not the paper's finding.** The authors argue that grizzly hunting on provincial
lands probably removes food-conditioned bears, excepting females with young (p. 53). Licensed
hunting would collapse under occupation while food waste rose. By the paper's own logic that
should raise the food-conditioned population over a multi-year occupation — a time-varying
encounter rate the model does not have. This is an extension of the authors' reasoning to a case
they did not study, and should be treated as a hypothesis.

**Scope.** Bears are 0.2–0.5% of US deaths in v0.1.2.6.1 and outcomes outside the Arctic scenario
move within noise. None of the recommendations below should be expected to move a headline result.
They are cheap corrections to a module whose sourcing is currently weaker than it needs to be,
and one of them replaces a citation to a pet-trivia website with a peer-reviewed census.

## Recommendation

R-001, R-002, R-003.
