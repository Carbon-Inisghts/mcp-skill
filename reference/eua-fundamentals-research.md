# EUA Fundamental Reasoning — External Research Validation

CarbonInsights desk scoreboard rules (emissions demand → EUA bias) align with EU ETS market structure and peer-reviewed / industry literature. Use this when explaining **why** `eua_bias` is labelled bullish or bearish.

> Desk labels describe **allowance demand fundamentals**, not guaranteed EUA **price** direction. Price can diverge short-term (positioning, policy, liquidity).

---

## Core law (validated)

**Higher verified emissions / compliance demand → bearish EUA fundamentals. Lower emissions / demand → bullish.**

| Source | Finding |
|--------|---------|
| [European Commission — About the EU ETS](https://climate.ec.europa.eu/eu-action/carbon-markets/about-eu-ets_en) | Cap-and-trade: declining cap + market price incentivises abatement; allowance scarcity drives compliance cost. |
| [ABN AMRO Carbon Market Strategist (2026)](https://www.abnamro.com/research/en/our-research/carbon-market-strategist-supply-uncertainty-and-weaker-demand-reshape-carbon) | Weaker emissions **demand** outlook contributed to softer EUA prices; traders cut longs as demand expectations fell. |
| [ETC/EIONET ETS Report 2025](https://www.eionet.europa.eu/etcs/etc-cm/products/etc-cm-report-2025-06/) | Verified emissions vs allowance supply balance drives market tightness; power-sector decarbonisation reduced emissions. |

**Desk rule:** Power/industry/aviation/maritime **emissions ↓** → **Bullish** (even −2% / −3.7%). **Emissions ↑** → **Bearish**.

---

## Power load ↑ → bearish

| Source | Finding |
|--------|---------|
| [Eslahi et al. — electricity demand & EUA (Ecological Economics, 2023)](https://ideas.repec.org/a/eee/ecolec/v214y2023ics0921800923002483.html) | Electricity demand among the most important predictors of EUA prices across EU ETS phases. |
| [Erasmus MSc thesis — demand drivers Phase IV](https://thesis.eur.nl/pub/69970/Master-Thesis-526197-.pdf) | Higher electricity demand → more fossil dispatch → upward pressure on carbon prices. |

**Desk rule:** Load **+8.6%** → **Bearish** ✓

---

## Solar / renewables ↑ → bullish (not bearish)

| Source | Finding |
|--------|---------|
| [ScienceDirect — EU ETS & renewables (2025)](https://www.sciencedirect.com/science/article/abs/pii/S014098832500475X) | EU ETS significantly increased renewable share and reduced fossil share in electricity mix. |
| [Renewable Energy Institute column (2024)](https://www.renewable-ei.org/en/activities/column/REupdate/20241219.php) | Higher RE + nuclear output **reduces fossil generation**, lowering **demand for emission allowances** and EUA price pressure. |
| [Eurelectric — What is an ETS?](https://www.eurelectric.org/in-detail/what-is-an-emission-trading-system/) | Merit order ranks renewables first; wind/solar displace fossil hours → lower power-sector emissions. |

**Desk rule:** Solar **+19%** → **Bullish** ✓ (displaces fossil burn). Labelling solar up as bearish is **wrong**.

---

## Fossil gas / coal generation ↑ → bearish (with fuel-switch nuance)

| Source | Finding |
|--------|---------|
| [Cambridge EPRG — fuel switching & merit order](https://www.jbs.cam.ac.uk/wp-content/uploads/2023/12/eprg-wp1107.pdf) | Carbon price + fuel prices determine coal vs gas merit-order switch; switching changes emissions and allowance demand. |
| [KU Leuven — Fuel switching in EU ETS](https://www.mech.kuleuven.be/en/tme/research/energy_environment/pdf/WPEN2007-04) | Coal→gas switch **lowers** GHG emissions per MWh; sufficient EUA price triggers switching. |
| [Montel — Carbon prices & merit order](https://montel.energy/resources/blog/how-carbon-prices-shape-power-markets) | Higher EUA costs push coal down merit order; gas vs coal breakeven drives dispatch. |

**Desk rule:** Fossil gas gen **+21%** (absolute rise) → **Bearish** ✓

**Nuance:** Gas **replacing** coal can be **bullish** for EUA (net emissions down). Use `analyze_fuel_switch` — do not score gas and coal rows in isolation when the question is fuel switch.

---

## Aviation emissions ↓ → bullish

| Source | Finding |
|--------|---------|
| [European Commission — Aviation allocation](https://climate.ec.europa.eu/eu-action/carbon-markets/eu-emissions-trading-system-eu-ets/free-allocation/allocation-aviation-sector_en) | Aviation covered by EU ETS; operators must surrender allowances for verified CO₂. |
| [EASA — EU ETS aviation](https://www.easa.europa.eu/en/domains/environment/eaer/market-based-measures/eu-emissions-trading-system) | Higher aviation activity increases EUA purchases; carbon price incentivises abatement/SAF. |
| [Transport & Environment ETS Report 2026](https://uploads.transportenvironment.org/production/files/TE-ETS-Report-2026_08.05.2026.pdf) | Aviation exceeds sector cap → net importer of general EUAs from stationary/maritime pool. |

**Desk rule:** Aviation **−12.9%** → **Bullish** ✓

---

## Forward CO₂ forecast ↓ → bullish

| Source | Finding |
|--------|---------|
| ABN AMRO / BNEF demand projections (2026 outlook) | Forward emissions demand trajectory is a primary driver of medium-term EUA price paths. |
| EC ETS cap trajectory | Falling expected compliance needs align with tighter or looser market balance. |

**Desk rule:** Forward forecast **−5.3%** → **Bullish** ✓

---

## COT / positioning — price signal, not emissions

| Source | Finding |
|--------|---------|
| [Homaio — COT in EU ETS](https://www.homaio.com/post/what-is-the-commitment-of-traders-report-in-the-eu-ets) | Weekly positioning report; net long/short reflects market sentiment on EUA **price**. |
| [Homaio — COT & EUA prices 2024](https://www.homaio.com/post/the-commitment-of-traders-report-and-eua-prices-in-2024) | Investment funds net short correlated with price declines; short covering associated with price rebounds. |

**Desk rule:** COT short **−19%** (covering) → **Bullish** for **price/positioning** — separate block from emissions scoreboard.

---

## Known limitations (document in desk answers)

1. **Fundamentals ≠ price short-term** — policy (MSR, ETS review), liquidity, and positioning can move EUA against emissions trend ([ABN AMRO 2026](https://www.abnamro.com/research/en/our-research/carbon-market-strategist-supply-uncertainty-and-weaker-demand-reshape-carbon), [Homaio Antwerp summit note](https://www.homaio.com/post/eu-carbon-market-how-the-antwerp-summit-sparked-a-new-battle-for-europes-industrial-future)).
2. **Fuel switch** — gas↑ coal↓ can lower net emissions; use `analyze_fuel_switch` and `fundamentals_price_read`.
3. **Auction / OI / options rows** — market microstructure; neutral unless tied to clear demand narrative.
4. **CarbonInsights figures** — always from MCP tool output for this user; external research validates **logic**, not specific desk numbers.

---

## Scoreboard mistakes (literature-backed)

| Row | Wrong | Correct | Why |
|-----|-------|---------|-----|
| Emissions −3.7% | Neutral / Bearish | **Bullish** | Lower compliance demand ([EC ETS](https://climate.ec.europa.eu/eu-action/carbon-markets/about-eu-ets_en)) |
| Solar +19% | Bearish | **Bullish** | RE displaces fossils ([REI 2024](https://www.renewable-ei.org/en/activities/column/REupdate/20241219.php)) |
| Aviation −13% | Bearish | **Bullish** | Fewer aviation EUAs required ([EASA](https://www.easa.europa.eu/en/domains/environment/eaer/market-based-measures/eu-emissions-trading-system)) |

Use `eua_bias` + `eua_bias_rule` from `multi_table_desk_briefing` — do not relabel.
