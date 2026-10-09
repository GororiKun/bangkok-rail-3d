# Journey planner — 8 October 2026

The Journey button adds departure/destination selection on the map, station-name search, draggable A/B markers, rail/walk/drive modes, route geometry, journey steps and 15/30/45-minute reach colors. The previous Routes button is now Lines. Existing cameras, fares, service notices and time controls remain available.

## Data and accuracy

- **Walk / Drive:** routes, turn instructions and generalized isochrone polygons are requested from the global [Valhalla FOSSGIS community service](https://valhalla.openstreetmap.de/), using OpenStreetMap. Drive estimates have **no live traffic**. The service may be unavailable or rate-limited. Default pedestrian costing is used. Instructions are in English; common Thai road names are normalized to English and other Thai-only names are shown as "the local road", rather than inventing a translation. Selected points must connect to a nearby routable street; there is no straight-line route fallback on failure.
- **Rail route:** a time-dependent graph over the 196 station nodes and 20 interchange connections in the existing Atlas. Directional segment times, departure patterns and operating windows come from the existing RailSim model; see [timetable source review](TIMETABLE_REVIEW.md). The query uses an explicit Bangkok departure time and selected weekday/weekend service pattern, independently of the animation slider. There is no live departure or disruption feed.
- Rail access/egress considers up to three nearest station nodes within 3 km, checked using pedestrian road-network matrix durations. Connections over 45 minutes of walking are excluded. A station selected explicitly starts/ends at its mapped station center. This limited search is **not a guarantee of the fastest possible journey**.
- Rail paths include a 2-minute initial platform allowance, actual street-routing time plus 4 minutes at a selected interchange, and a 1-minute exit allowance. Selected access, egress and transfer legs are checked against detailed street routes. Matrix estimates are replaced by those returned durations, and rail connections and arrival times are recalculated until all selected walking legs agree with the itinerary. Map geometry follows the included track paths and the returned pedestrian paths. Station-center coordinates are not surveyed entrance coordinates; internal station circulation is approximated by the allowances.
- Queries stop at a 2-hour horizon. If no modeled connection exists in that period, the UI says so rather than manufacturing a train. It does not search for the following morning's first train.
- **Rail colors are schematic, not pedestrian-network isochrones.** Approximately 330 m cells represent modeled station arrival plus straight-line walking at 4.5 km/h, limited to 15 minutes of walking, including walking directly from the origin. They can cross water or inaccessible land. Unselected transfer walking remains modeled until checked for a selected route. Pick a destination to check street-based access and transfer walking. The map legend and planner explicitly distinguish this approximation from the Walk / Drive street-network contours.
- The colors represent travel-time bands, **not Bangkok administrative boundaries**. No district-level boundary or district-wide travel-time claim is made.

## Interaction

1. Open Journey. Choose a station, use the map center, or press Pick on map to place A.
2. A alone shows reach colors. Add B for a detailed route.
3. Choose Rail, Walk or Drive. Rail offers departure time and weekday/weekend/holiday pattern controls.
4. View on map closes the panel; reopen Journey to see the itinerary. On phones, the panel sits above the bottom dock and endpoint inputs collapse after a result.
5. Clear removes the route, colors and endpoints. Change departure time, mode or point to calculate another journey. Escape cancels map picking.

## Network, security and operation

Requests go directly to `https://valhalla1.openstreetmap.de` with an identifying `X-Client-Id: bangkok-rail-3d.netlify.app` header and no credentials. The CSP adds only that exact host to `connect-src`. All provider route text is HTML-escaped. No API keys, geolocation access, authentication or payment flows were introduced.

Requests are serialized at least 1.15 seconds apart, cached in memory (maximum 80 responses per tab), cancelled when superseded, and bounded by a 20-second network timeout. There is no background polling or bulk reachability collection. Selected coordinates and the normal request metadata are transmitted to the routing provider. The interface links to OpenStreetMap attribution and Fix the Map.

This is a community-service integration for light interactive use, without an availability guarantee. The provider's [public-server guidance](https://github.com/valhalla/valhalla#demo-server) asks apps to identify themselves and to let the maintainers know via GitHub Discussions. The identifying header is included; no external message was sent on the owner's behalf. A managed or self-hosted endpoint should be evaluated if usage grows.

The area interaction is inspired by [Camille Roux's Brussels travel-time map](https://tram.camilleroux.com/bruxelles/). Its code and assets were not copied.

## Validation

`work/verify-journey.cjs` checks rail waits, transfers, service closure, late running, the two Tha Phra visits, monotonic arrival times, invalid access costs, catchment bands and real returned route geometry decoding. Existing rail geometry/motion and service-alert provenance tests also pass.

Browser checks cover real street routes and contours for walking and driving, an actual no-service message at 02:00, smartphone layout at 390 × 844 without horizontal overflow, and minimum 51 px dock-button widths at that size. Final release verification is recorded in the task; a preview alone is not proof of production publication.

## Clear controls and route styling

Clear A / B is visible above the Journey controls after either point is set, and directly on the map when the panel is closed. It cancels pending calculations and removes both endpoints, the route and reach colors. Each endpoint also has Clear A or Clear B inside the endpoint editor. Clearing one retains the other without issuing another request.

All selected journeys use a solid magenta path with a white outline and repeated direction chevrons. This is independent of railway line colors and does not use MRT-style tunnel dashes. Mode and transfer details remain in the itinerary.
