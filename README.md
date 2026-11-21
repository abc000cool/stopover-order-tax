# The Itinerary Order Tax

When you visit several cities on one trip, the order you visit them in changes what the flights cost. Most people type the order they first thought of. This dataset measures what that costs, on real trips planned on [Stopover](https://flystopover.com), a multi-city trip planner that prices every order of a trip's cities.

**Live version, charts and the latest numbers: [flystopover.com/order-tax](https://flystopover.com/order-tax)**

## The findings (version of November 11, 2026)

On **197** real multi-city trips planned between September and November 2026, from **70** home airports:

- **56%** were typed in an order that cost more than the cheapest order of the same cities.
- Among those, the median extra cost was **$123 a person**, about 13% of their flights.
- Averaged over every trip, including the 44% that had already picked the cheapest order, the order cost **$95 a person**.
- One trip in ten paid **$258 a person or more**.
- The tax grows with the trip: trips of 2 cities paid an average of $59 a person; trips of 5 or more cities paid $140, with a median of $213 among those that paid one.

Same cities, same travelers, same window of dates. The only thing that differs between the two prices is the order the cities are visited in.

## The data

[`data/order-tax.csv`](data/order-tax.csv) holds one row per trip:

| Column | Meaning |
|---|---|
| `home` | Home airport or metro code |
| `cities` | The cities visited, space separated, in the order the traveler typed them |
| `region` | Region of the trip |
| `travel_month` | The month the travel window starts |
| `window_days` | How many days the travel window is |
| `travelers` | Number of travelers |
| `typed_order_per_person_usd` | Flights for the typed order, per person, US dollars |
| `cheapest_order_per_person_usd` | Flights for the cheapest order of the same cities, per person |
| `gap_usd` | The order tax: typed minus cheapest, never below zero |
| `orders_ranked` | How many orders the plan kept |
| `planned_month` | The month the plan was made |

No names, accounts, exact dates, plan ids or fares by leg: a list of cities and a month is a trip, not a person.

## How it was measured

Every trip is a plan someone made on Stopover: a home airport, two or more cities typed in some order, a window of dates, a range of nights per city and a number of travelers. The planner prices the typed order and every other order on dates that fit inside the window, per person, using the same fares for both, and keeps the cheapest. The order tax is the typed order's price minus the cheapest order's price, never below zero.

Prices are flights only, per person, in US dollars, from cached fares and from live searches where the plan ran them. They are the fares that were on sale when the plan ran, not booked tickets. Where a plan was ranked for a balance of price and time rather than price alone, a cheaper order may have ranked below the ones kept, so the tax is, if anything, understated.

Left out: trips with one city (there is no order to choose), demonstration plans, plans the person stopped early, Stopover's own test trips, and trips where the typed order or the cheapest one was priced partly from an estimate rather than a quoted fare. The same trip planned more than once counts once, the latest time. For this version, 405 finished plans were read and 197 trips remain after the exclusions.

The dataset is rebuilt as trips accumulate. This repository mirrors the published version; the [live page](https://flystopover.com/order-tax) always has the latest.

## License and citation

Free to use and publish under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) with a link to [flystopover.com/order-tax](https://flystopover.com/order-tax).

> Stopover. "The Itinerary Order Tax." Updated November 11, 2026. https://flystopover.com/order-tax

In one sentence: *On 197 real multi-city trips, 56% were typed in an order that cost more than the cheapest order of the same cities, by a median of $123 a person.*

Questions about the data: anshpathak@flystopover.com
