# Binwise hackathon pitch kit

**Collect by need. Keep the city moving.**

## Two-minute spoken pitch

Imagine two streets in the same city. On one, a garbage truck stops at a half-empty bin. On the other, waste is overflowing and nobody knows. The city already has trucks. What it lacks is timely information about where to send them.

We built Binwise, a demand-based waste collection platform. Our working prototype simulates twenty-four bins across Kolkata and four municipal trucks. It brings sensor readings, citizen reports and collection planning into one control centre.

Here is what makes the decision smarter than a simple fill threshold. We estimate how long each bin has before it becomes full, using its remaining capacity and waste accumulation rate. We combine that forecast with fill level, collection age, area activity and citizen reports. A fast-filling bin can therefore become urgent before it looks full.

The operator generates a route, reviews the stops and dispatches an available truck. The planner prioritises critical bins, favours nearby stops and respects truck capacity. As we advance simulated time, waste builds up, trucks complete collections and alerts change. Residents can report missed collections, while damaged-bin reports stay open for maintenance.

In our starting scenario, Binwise selects eight stops instead of twenty-four. Estimated distance falls from seventy-four kilometres to about forty-eight, saving roughly seven litres of fuel for that dispatch. These are transparent simulation estimates. Some collection is deferred, so we are not claiming full-day or real-world savings.

We would pilot this in one ward, compare service reliability and total operating cost, then connect real sensors and GPS only where they add value. Our prototype uses explainable rules, not a pretend machine-learning model.

Cities do not necessarily need more garbage trucks. They need better information about where those trucks should go. Binwise helps them collect by need.

*Approximately 285 words. Rehearse at about 140–145 words per minute, allowing a brief pause for the live route generation.*

## Thirty-second elevator pitch

Binwise helps municipal trucks collect waste where it is needed most. It combines bin levels, overflow forecasts and citizen reports to prioritise collection, then assigns capacity-aware routes. Our Kolkata prototype includes a live city simulation, so you can watch bins fill and trucks respond. In one clearly labelled simulation, it reduces dispatch distance by about thirty-five percent. We propose a ward-level pilot to measure actual service and cost improvements.

## Demo choreography

1. **Start from Reset at 08:00.** Show 24 bins, 8 requiring collection, 2 critical bins and 3 available trucks.
2. **Click B-07, Burrabazar.** Explain 98% fill, 600 L capacity, 14 L/hour growth and roughly 0.9 hours to full.
3. **Generate route.** Show 8 stops, 48.3 km and 13.8 L estimated fuel versus 24 stops, 74.0 km and 21.2 L. Clarify that the baseline is fixed bin-ID order, with identical capacity and distance assumptions.
4. **Dispatch, then +4 hours.** Open Fleet. The truck has collected approximately 5,041 L, including growth before arrival, and returned to depot.
5. **Citizen report.** Choose B-11 Maidan, select Missed collection, enter “Waste pickup missed near the park entrance.” Submit and regenerate a plan. This demonstrates that reports influence priority independently of fill.
6. **Optional counterfactual.** Reset and advance +4 hours without dispatch. Five bins have reached full capacity. Do not describe this no-dispatch scenario as a measured traditional-route result.
7. **Close.** Return to a fresh reset state so the next judge can explore.

If the live demo has a connection issue, run the included prebuilt `dist` app with the README instructions. The engine and demo do not need a routing API or sensor hardware. Browser fonts may fall back offline.

## Impact you can defend

| Metric | Traditional snapshot | Binwise snapshot | Interpretation |
|---|---:|---:|---|
| Stops | 24 | 8 | Demand-based selection defers low-priority stops |
| Distance | 74.0 km | 48.3 km | 25.8 km / 34.8% less for this dispatch |
| Fuel | 21.2 L | 13.8 L | 7.4 L estimated saving at 3.5 km/L |
| Fuel cost | ₹2,010 | ₹1,310 | About ₹700 less using assumed ₹95/L |
| Selected waste | 10,922 L | 4,820 L | Different collection scope, not like-for-like volume |
| Selected volume per kilometre | 147.5 L/km | 99.8 L/km | This metric does NOT improve in this snapshot |
| Initial priority bins selected | 8 of 8 | 8 of 8 | Both include priority bins, but order and time differ |

Separate four-hour counterfactual: **five bins reach full with no dispatch, zero with the generated smart dispatch**. This does not establish superiority to the fixed-route baseline on overflow, because that baseline was not simulated in this counterfactual. The live app's “at-risk bins serviced” counter is a proxy based on forecast at pickup, not a causal prevention count. Historical charts are explicitly illustrative.

## Likely judge questions and answers

**1. Is this AI?**
No machine learning is in the prototype. We use a transparent forecast, weighted priority rules and a route heuristic. A future model should earn its place by improving forecast accuracy over this baseline.

**2. How do you predict overflow?**
Remaining bin volume divided by estimated litres added per hour. The current simulator uses a fixed rate. In production we would estimate rates from cleaned recent readings and evaluate forecast error across locations and times of day.

**3. Why not just collect bins over 80%?**
Two 70%-full bins can have very different deadlines if one is filling five times faster. Capacity, local activity, time since service and reports also matter. The UI exposes the score and predicted time-to-full.

**4. Is the route optimal?**
No. It is a capacity-aware, priority-weighted nearest-neighbour heuristic. Critical bins rank first; distance then helps choose among candidates. We would use a vehicle-routing solver and a road travel-time matrix at production scale.

**5. How credible are the savings?**
They are reproducible model outputs for a disclosed synthetic snapshot. The comparison uses the same depot, road factor, fuel economy and truck capacities, but different service scopes. We need a whole-day field pilot and a stronger optimised baseline before claiming operational savings.

**6. Does collection efficiency improve?**
It depends on the metric. We reduce stops and distance for the chosen dispatch, but litres per kilometre is actually lower in the starting scenario. We prioritise service urgency and report the trade-off rather than selecting only favourable metrics.

**7. What if every bin becomes critical?**
The planner fills available truck assignments without exceeding their volume limit. Bins that do not fit remain explicitly unassigned. After trucks return and unload, the operator can dispatch again. Arrival deadlines and extra shifts are future constraints.

**8. What if sensors fail or readings are wrong?**
The production design needs timestamp validation, stale-reading alerts, device-health monitoring and a fallback service schedule. Citizen reports supplement telemetry. The current prototype does not simulate sensor failures.

**9. How do you stop false reports?**
This local demo accepts reports for demonstration. A live service would need rate limiting, deduplication, moderation and corroboration from sensor readings or crew confirmation. Citizen reports should influence operator review, not become unquestioned truth.

**10. What happens to waste segregation?**
The demo displays waste types but treats the trucks as generic volume containers. A real planner must match waste streams to compatible vehicles and disposal facilities, and enforce mass limits as well as volume.

**11. Do you need sensors on every bin?**
No. Start with high-variation or problem locations and combine those readings with crew observations and reports. Compare the value of more sensors against maintenance and connectivity costs.

**12. What is the implementation model?**
A paid ward-level pilot with installation and support, then an annual platform and maintenance contract if service targets are met. Hardware can be supplied through partners. Pricing needs local procurement and operating-cost evidence; we are not presenting invented contract values.

**13. What makes this different from a map of smart bins?**
The prototype connects observations to an actionable decision: forecast urgency, explain priority, select stops, allocate capacity, dispatch and record collection outcomes. The complete feedback loop is the product.

**14. What would you measure in a pilot?**
Overflow duration, missed critical collections, total daily vehicle kilometres, litres of fuel, cost per tonne, time to resolve reports, sensor uptime and forecast error. Compare matched wards or alternate comparable periods, controlling for weekends and demand.

**15. What is your next milestone?**
Run the same scenarios against an optimised all-bin baseline, add deadline-aware scheduling and waste-stream compatibility, then validate forecasts using actual bin readings from a small field trial.

## Proposed rollout and commercial model

- Weeks 1–2: map one ward's bins and vehicle constraints, capture current routes and service outcomes, agree success measures.
- Weeks 3–4: trial telemetry on selected bins and run recommendations in shadow mode while crews follow existing operations.
- Weeks 5–8: let operators approve demand-based routes, preserve emergency overrides, and evaluate whole-day service and cost.
- Expansion gate: proceed only if reliability and operating economics improve enough to justify sensors, upkeep and software.
- Buyer: municipal sanitation department or its collection contractor. Revenue hypothesis: setup, annual software, support and optional device maintenance. Pilot duration and model are proposals, not commitments or validated market evidence.
