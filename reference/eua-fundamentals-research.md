# EUA Fundamental Reasoning — External Research Validation

CarbonInsights desk rules map **allowance demand** to **EUA price** bias (bullish = price support, bearish = price pressure). Use this when explaining **why** `eua_bias` is labelled bullish or bearish.

> **Bullish/bearish = EUA price** for the long desk. Price can diverge from the latest emissions print short-term — use `fundamentals_price_read`.

---

## Core law (validated)

**Higher verified emissions / compliance demand → bullish EUA price. Lower emissions / demand → bearish EUA price.**

| Source | Finding |
|--------|---------|
| [European Commission — About the EU ETS](https://climate.ec.europa.eu/eu-action/carbon-markets/about-eu-ets_en) | 2008 crisis: emissions fell more than expected → large allowance surplus → **weighed heavily on the carbon price**. |
| [ABN AMRO Carbon Market Strategist (2026)](https://www.abnamro.com/research/en/our-research/carbon-market-strategist-supply-uncertainty-and-weaker-demand-reshape-carbon) | Weaker emissions **demand** outlook contributed to **softer EUA prices**. |
| [KU Leuven — COVID demand shock & EU ETS](https://www.mech.kuleuven.be/en/tme/research/energy-systems-integration-modeling/pdf-publications/wp-esim2020-09) | Negative demand shock **decreases the price of emission allowances** under cap-and-trade. |
| [EC — Market Stability Reserve](https://climate.ec.europa.eu/eu-action/carbon-markets/eu-emissions-trading-system-eu-ets/market-stability-reserve_en) | 2008 crisis → lower emissions than anticipated → **lower demand for allowances** → surplus → lower prices. |

**Desk rule:** Power/industry/aviation/maritime **emissions ↑** → **Bullish** EUA price. **Emissions ↓** → **Bearish** (even −2% / −3.7%).

---

## Emissions down → price down (user FAQ)

Yes — in fundamentals terms, **lower emissions mean lower allowance demand**, which tends to **pressure EUA price lower** (bearish). That is why emissions **−3.7%** is **bearish**, not bullish.

**When price falls but emissions have not fallen:** use `fundamentals_price_read` — drivers may include MSR/auction supply, positioning, forward cap narrative, or sentiment while the latest emissions print is flat or still rising ([Gerlagh & Heijmans — MSR & COVID](https://link.springer.com/article/10.1007/s10640-020-00441-0)).

---

## Power load ↑ → bullish EUA price

| Source | Finding |
|--------|---------|
| [Eslahi et al. — electricity demand & EUA (Ecological Economics, 2023)](https://ideas.repec.org/a/eee/ecolec/v214y2023ics0921800923002483.html) | Electricity demand among the most important predictors of EUA prices. |
| [Erasmus MSc thesis — demand drivers Phase IV](https://thesis.eur.nl/pub/69970/Master-Thesis-526197-.pdf) | Higher electricity demand → more fossil dispatch → upward pressure on carbon prices. |

**Desk rule:** Load **+8.6%** → **Bullish** ✓

---

## Solar / renewables ↑ → bearish EUA price

| Source | Finding |
|--------|---------|
| [Renewable Energy Institute column (2024)](https://www.renewable-ei.org/en/activities/column/REupdate/20241219.php) | Higher RE output **reduces fossil generation**, lowering **demand for emission allowances** and **EUA price**. |
| [Eurelectric — What is an ETS?](https://www.eurelectric.org/in-detail/what-is-an-emission-trading-system/) | Merit order ranks renewables first; wind/solar displace fossil hours. |

**Desk rule:** Solar **+19%** → **Bearish** EUA price ✓ (metric + is green; EUA column red).

---

## Fossil gas / coal generation ↑ → bullish (with fuel-switch nuance)

| Source | Finding |
|--------|---------|
| [Cambridge EPRG — fuel switching & merit order](https://www.jbs.cam.ac.uk/wp-content/uploads/2023/12/eprg-wp1107.pdf) | Dispatch changes emissions and allowance demand. |
| [Montel — Carbon prices & merit order](https://montel.energy/resources/blog/how-carbon-prices-shape-power-markets) | Higher EUA costs push coal down merit order. |

**Desk rule:** Fossil gas gen **+21%** (absolute rise) → **Bullish** ✓

**Nuance:** Gas **replacing** coal can lower net emissions → use `analyze_fuel_switch`.

---

## Aviation emissions ↓ → bearish EUA price

| Source | Finding |
|--------|---------|
| [EASA — EU ETS aviation](https://www.easa.europa.eu/en/domains/environment/eaer/market-based-measures/eu-emissions-trading-system) | Higher aviation activity increases EUA purchases. |

**Desk rule:** Aviation **−12.9%** → **Bearish** ✓

---

## Forward CO₂ forecast ↑ → bullish

**Desk rule:** Forward forecast **+5%** → **Bullish** | forecast **−5%** → **Bearish**

---

## COT / positioning — price signal, not emissions

Separate scoreboard block from emissions fundamentals ([Homaio — COT in EU ETS](https://www.homaio.com/post/what-is-the-commitment-of-traders-report-in-the-eu-ets)).

---

## Scoreboard mistakes (literature-backed)

| Row | Wrong | Correct | Why |
|-----|-------|---------|-----|
| Emissions −3.7% | Bullish / Neutral | **Bearish** | Lower compliance demand → price pressure ([EC ETS](https://climate.ec.europa.eu/eu-action/carbon-markets/about-eu-ets_en)) |
| Solar +19% | Bullish | **Bearish** | RE displaces fossils ([REI 2024](https://www.renewable-ei.org/en/activities/column/REupdate/20241219.php)) |
| Aviation −13% | Bullish | **Bearish** | Fewer aviation EUAs required |
| Fossil gas +21% | Bearish | **Bullish** | Higher burn → more allowance demand |
| Load +8.6% | Bearish | **Bullish** | Higher demand → more emissions pressure |

Use `eua_bias` + `eua_bias_rule` from `multi_table_desk_briefing` — do not relabel.
