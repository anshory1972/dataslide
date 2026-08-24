# Structural transformation charts

Two charts on one axis: the share of a sector in value added against GDP per
capita in **constant 2015 US dollars**, log scale.

1. **Growth comes from productivity** — labour productivity growth split into
   within-sector gains and structural change, for seven Asian economies in their
   growth spell and in 2012–2018.

2. **Agriculture** — 202 countries at their latest year, 38 Indonesian provinces
   in 2024, and Indonesia's own path from 1960.
3. **Manufacturing** — the path of each Indonesian province since 2010, of
   Indonesia since 1983, and of six international benchmarks.
5. **Aceh: what raises growth** — the growth gain from each of the thirteen
   scenarios simulated with IndoTERM Aceh.

6. **Kepulauan Riau: diversifying takes more than investment** — the gain from
   directing the same investment at each sector, against the electronics
   benchmark, and the extra demand each alternative needs to match it.

7. **The challenge of global fragmentation** — four panels: world trade as a share of
   GDP, new trade restrictions per year, far-right vote share since 1900, and
   far-right seat share by country. Data from *The Growth We Want*.

4. **Output per head and poverty** — Sulawesi Tengah, Maluku Utara and Indonesia
   by year: GRDP per capita at constant 2012 prices on the left axis, poverty
   headcount on the right.

Build with `python deck.py`, which reads `csv/` and writes
`structural-transformation.html`. Published at
<https://anshory1972.github.io/dataslide/structural-transformation.html>.

## Folders

| Folder | What is in it |
|---|---|
| `csv/` | The processed inputs the charts actually read. One file per chart layer. |
| `rawdata/worldbank_api/` | World Bank API responses, unmodified JSON. |
| `rawdata/bps_api/` | BPS Web API responses, unmodified JSON, one file per variable and year. |

## csv/

| File | Rows | Contents |
|---|---|---|
| `chart1_countries_agriculture.csv` | 202 | One row per country: income per head and agriculture's share, at the most recent year reporting both. |
| `chart1_indonesia_agriculture.csv` | 65 | Indonesia 1960–2024. `basis` is `current` from 1983, `constant` before that (see below). |
| `chart1_provinces_agriculture.csv` | 38 | Provinces in 2024, with both the original rupiah figure and the converted one. |
| `chart2_provinces_manufacturing.csv` | 511 | Every province in every year 2010–2024. |
| `chart2_indonesia_manufacturing.csv` | 42 | Indonesia 1983–2024. |
| `chart2_benchmarks_manufacturing.csv` | 780 | 18 countries and country groups; `shown_on_chart` marks the six drawn. |
| `chart3_regions_income_welfare.csv` | 75 | Five regions by year (three are drawn; Jawa Barat and Banten are kept for reuse): GRDP per capita and adjusted expenditure per capita, both at constant 2012 prices, plus poverty and Gini. The chart draws GRDP per capita and poverty; the other two columns are kept for reuse. |
| `chart9_four_strategies.csv` | 4 | The four strategies, which is highlighted, and its artwork file. |
| `chart9_strategic_shift.csv` | 3 | The three components of Strategic Shift. |
| `chart10_sat_pillars.csv` | 4 | The four pillars of Strategic Agricultural Transformation. |
| `chart6_aceh_scenarios.csv` | 13 | Aceh scenarios: growth reached and gain over baseline. |
| `chart7_kepri_pathways.csv` | 5 | Kepri sectors: gain from investment alone, and the extra demand needed to reach +0.5pp. |
| `chart5_growth_decomposition.csv` | 14 | Seven countries, two periods each: productivity growth split into within-sector and structural-change components. |
| `chart5_structural_change_decomposition.csv` | 51 | The same decomposition, 1990–2018, for every country in the ETD. |
| `chart4_globalisation_populism.csv` | 197 | Trade as % of GDP, trade restrictions by type, and vote share by party family. |
| `chart4_farright_seats.csv` | 11 | Seat share of the largest far-right party, latest lower-house election. |
| `conversion_anchor.csv` | 10 | The rupiah-to-dollar factor used, by year. |

## Two things worth knowing before reusing the data

**Provincial income per head is converted, not exchanged.** BPS publishes
provincial GRDP per head only in current rupiah. Each province is scaled by the
ratio of Indonesia's GDP per head in constant 2015 US dollars to its GDP per head
in current rupiah, **in that same year** — Rp 17,879 per constant-2015 dollar in
2024, against a market rate of Rp 15,855 per current dollar. Using the market
rate would put every province about 13% too high. Provincial relativities stay
exactly as BPS reports them and the national level is the World Bank's.

**Indonesia's agriculture path before 1983 is a different measure.** The World
Bank's current-price agriculture share starts in 1983. The years 1960–1982 use
agriculture value added over GDP with both in constant local currency, which
differs from the current-price measure by 0.8 percentage points on average over
the 42 years in which both exist. The `basis` column says which is which, and the
chart draws the earlier segment dashed.

**The two per-capita series are put on one price base.** BPS publishes GRDP per
capita at constant 2010 prices and adjusted expenditure at constant 2012 prices.
The GRDP series is multiplied by Indonesia's implicit 2012 GDP deflator, 1.1211,
computed from the national current- and constant-price series. The national
deflator is used for provinces too, because the expenditure measure is itself
adjusted to a single national basis.

Two further limits: the provincial series cannot start before 2010, the first
year of the 2010-base regional accounts; and summing provincial PDRB gives a
manufacturing share 2.6 points above the national figure in 2010, widening to 4.3
points by 2024, because provincial accounts and national GDP differ in coverage
and in the treatment of taxes on products.

Slide 1 uses the GGDC / UNU-WIDER **Economic Transformation Database** (ETD,
18 September 2023): value added at constant 2015 prices and employment for twelve
sectors in 51 countries, 1990–2018, held in `rawdata/etd/`. The decomposition
follows McMillan and Rodrik and reproduces `rawdata/etd/ggdc.do`; within and
structural terms sum exactly to the change in economy-wide productivity, verified
to a residual of 1.5e-11. Productivity is in national currency, so growth rates
compare across countries but levels do not.

8. **The grand strategy** — an illustrated divider.

9. **Where transmigration sits** — the four strategies, with Strategic Shift and,
   inside it, Strategic Agricultural Transformation, where transmigration areas fall.

10. **The four pillars of SAT**.

Slides 8 to 10 draw on the author's own decks in `refs/` — the divider image is
Midjourney in the deck's risograph style, the four-strategy artwork is lifted from
`iesp-seminar-aay.pptx` slide 6, and the SAT content from its slides 8 and 9.

The page is **locked to light mode**: the house style flips its whole palette
under `prefers-color-scheme: dark` and `[data-theme="dark"]`, so `deck.py` pins
the effective light values — the FT palette at the end of `_house_style.css`, not
the earlier `scope-slide2` one it supersedes. Verified identical under a dark
system setting and under an explicit dark theme attribute.

## Sources

World Bank World Development Indicators: `NY.GDP.PCAP.KD`, `NY.GDP.PCAP.CN`,
`NV.AGR.TOTL.ZS`, `NV.AGR.TOTL.KD`, `NY.GDP.MKTP.KD`, `NV.IND.MANF.ZS`.

Slide 4 is taken from *The Growth We Want* (`E:\summerschool2026
eplicate`),
which draws on the World Bank, Global Trade Alert, ParlGov and IPU Parline.

BPS Web API: variable 2268 (PDRB by 17 industry categories, current prices, by
province), variable 288 (GRDP per capita), variable 416 (adjusted expenditure per
capita, the consumption component of the new-method HDI), variable 192 (percentage
of poor population, P0) and variable 98 (Gini ratio). Poverty and
Gini are the **March** round throughout; BPS also publishes September, and the two
rounds are not comparable. The provincial March poverty series begins in 2012.
