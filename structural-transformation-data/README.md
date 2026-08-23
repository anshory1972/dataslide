# Structural transformation charts

Two charts on one axis: the share of a sector in value added against GDP per
capita in **constant 2015 US dollars**, log scale.

1. **Agriculture** — 202 countries at their latest year, 38 Indonesian provinces
   in 2024, and Indonesia's own path from 1960.
2. **Manufacturing** — the path of each Indonesian province since 2010, of
   Indonesia since 1983, and of six international benchmarks.
3. **Output per head and poverty** — Sulawesi Tengah, Maluku Utara, Jawa Barat,
   Banten and Indonesia by year: GRDP per capita at constant 2012 prices on the
   left axis, poverty headcount on the right.

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
| `chart3_regions_income_welfare.csv` | 75 | Five regions by year: GRDP per capita and adjusted expenditure per capita, both at constant 2012 prices, plus poverty and Gini. The chart draws GRDP per capita and poverty; the other two columns are kept for reuse. |
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

## Sources

World Bank World Development Indicators: `NY.GDP.PCAP.KD`, `NY.GDP.PCAP.CN`,
`NV.AGR.TOTL.ZS`, `NV.AGR.TOTL.KD`, `NY.GDP.MKTP.KD`, `NV.IND.MANF.ZS`.

BPS Web API: variable 2268 (PDRB by 17 industry categories, current prices, by
province), variable 288 (GRDP per capita), variable 416 (adjusted expenditure per
capita, the consumption component of the new-method HDI), variable 192 (percentage
of poor population, P0) and variable 98 (Gini ratio). Poverty and
Gini are the **March** round throughout; BPS also publishes September, and the two
rounds are not comparable. The provincial March poverty series begins in 2012.
