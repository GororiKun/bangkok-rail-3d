# Bangkok Rail Atlas

Service notices were added on 7 September 2026. The map supports persistent affected-station warnings and source links, but a continuous operator disruption feed is not connected. The shipped collection reports unknown status. See [Service notice sources and limitations](SERVICE_ALERTS.md). Keep `service-alerts.json` next to the HTML when hosting it.

Open `index.html` in a modern browser. Internet access is required for background maps, roads, buildings and satellite imagery. Rail geometry and rendering libraries are embedded in the HTML.

## Updated controls

- **Fares & times** opens a mobile-friendly journey desk for station-pair fares, published terminal first/last trains, effective dates and source links. See [18 September 2026 source review](TIMETABLE_REVIEW.md) for coverage and limitations.

- The app starts at the current Bangkok time (UTC+7), continuously synchronized at 1× speed. `Now` restores this mode after exploring another time. The device clock must be correct.
- `Train size` offers Medium, Large (default) and Extra large. Train symbols remain visible when zoomed out; detailed trains appear when zoomed in.
- Select a train to see its estimated speed in km/h, destination and next stop. `Follow train` moves the camera closer; dragging the map stops following.
- `Night` lights the windows, headlights and red tail lights, with a glow around the trains.
- Use Map, Satellite and Night for different backgrounds. Roads, station names, controls and information panels use English labels. Underlying search data also accepts Thai station names.
- Use the time slider, playback speed and weekday/weekend controls to explore service. These leave current-time synchronization; press `Now` to return.
- Use the menu on small screens for line selection and station search. The information button explains sources and limitations.

## What the train positions mean

**Positions and speeds are timetable-informed estimates, not live train telemetry. No verified continuous live feed is connected.** The app cannot show actual train IDs, delays, cancellations or live arrival predictions.

The model includes acceleration, cruising, braking, station dwell times, direction-specific departures where available, peak/off-peak intervals and trips continuing after midnight. BEM Blue and Purple travel times use differences between minute-rounded published last-train station times; missing terminal arrival intervals are approximated. BTS Gold uses the currently published 8/10/15-minute pattern (July 2023 edition). Other services combine published headways and representative running assumptions.

The review on 18 September 2026 supersedes the older BTS PDFs linked by the English landing page: Green headways now use the January 2026 edition and Gold uses July 2023. Red terminal departures use explicit operator tables. BEM weekday terminals were rechecked on 18 September; weekend values retain the 6 September snapshot. Weekends are detected automatically, but Thai public holidays require manual selection. See the source review for unresolved coverage.

Short workings, intermediate-origin first trains, depot movements, extra services, cross-line workings and real-time disruptions are not reproduced. This is a geographic rail visualizer, not a passenger journey-planning or operational control system.

## Geographic detail

11 services, 197 stop-order entries, 196 station markers and 2,703 track geometry points are included. OSM coordinates and route relations replace schematic station-to-station curves. Major roads, rivers, parks and building footprints come from the background map. Twenty transfer connections preserve the distinct positions of connecting stations.

Elevated heights, tunnel depths, station structures, piers and vehicles are simplified. Vehicle sizes and lateral separation are exaggerated for visibility. Underground trains use a surface projection. Building heights can include estimates. Transfer links are approximate station-center connections, not measured walking paths. Night mode is a rendered theme, not nighttime photography. Google Earth was used for visual reference; its photogrammetric models were not copied.

## Verification

69,113 sampled train states passed finite-position and speed-range checks in both directions. Stopped trains have zero speed; phase transitions preserve position. Geometry checks found no route gaps and a maximum 40.2 m separation between station centers and their track projections. This measures consistency between the included datasets, not survey accuracy. Overnight trips remain active after midnight and the modeled services finish by 02:00.

Earlier browser checks confirmed current-time synchronization, English controls, enlarged symbols and Night rendering. The final follow-camera adjustment has passed syntax checks but its final close-up appearance could not be rechecked because the browser security policy blocked opening the local HTML.

## Sources and credits

- [Bangkok Transit Map — Oran Viriyincy](https://www.bangkoktransitmap.com/): reference map for lines and interchanges.
- [Google Earth / Bangkok](https://earth.google.com/web/@13.75,100.54,0a,40000d,35y,0h,45t,0r): visual geographic reference.
- [BTS timetable page](https://www.bts.co.th/eng/service/timetable.html)
- [BTS Green Line timetable, effective 1 January 2026](https://www.ebm.co.th/cms-routemap/WareHouse/TimeTable/GreenLine.pdf)
- [BTS Gold Line timetable, effective 1 July 2023](https://www.ebm.co.th/cms-routemap/WareHouse/TimeTable/GoldLine.pdf)
- [BEM timetable and fare calculator](https://metro.bemplc.co.th/Fare-Calculation?lang=en)
- [BEM system map](https://metro.bemplc.co.th/MRT-System-Map)
- [MRTA operating lines](https://www.mrta.co.th/en/opening)
- [Yellow Line timetable](https://www.ebm.co.th/cms-routemap/WareHouse/TimeTable/YellowLine.pdf)
- [Pink Line and Muang Thong Thani timetable](https://www.ebm.co.th/cms-routemap/WareHouse/TimeTable/PinkLine.pdf)
- [SRTET Red Line timetable](https://www.srtet.co.th/en/fare-timetable)
- [OpenStreetMap contributors / ODbL](https://www.openstreetmap.org/copyright): rail data retrieved 6 September 2026.
- [OpenFreeMap](https://openfreemap.org/) and [OpenMapTiles](https://openmaptiles.org/): roads, labels, rivers and buildings.
- [Esri World Imagery](https://www.arcgis.com/home/item.html?id=10df2279f9684e4a9f6a7f08febac2a9): satellite imagery; Esri, Maxar, Earthstar Geographics and the GIS User Community.
- MapLibre GL JS 5.6.2 and Three.js r128; library license notices are retained in the HTML.

## OSM route relations

| Service | OSM relation |
|---|---|
| BTS Sukhumvit | [444651](https://www.openstreetmap.org/relation/444651) |
| BTS Silom | [2067854](https://www.openstreetmap.org/relation/2067854) |
| BTS Gold | [11681439](https://www.openstreetmap.org/relation/11681439) |
| MRT Blue | [444659](https://www.openstreetmap.org/relation/444659) |
| MRT Purple | [7725057](https://www.openstreetmap.org/relation/7725057) |
| MRT Yellow | [15806897](https://www.openstreetmap.org/relation/15806897) |
| MRT Pink | [16740886](https://www.openstreetmap.org/relation/16740886) |
| Muang Thong Thani spur | [19149752](https://www.openstreetmap.org/relation/19149752) |
| Airport Rail Link | [2148241](https://www.openstreetmap.org/relation/2148241) |
| SRT Dark Red | [13058384](https://www.openstreetmap.org/relation/13058384) |
| SRT Light Red | [14071495](https://www.openstreetmap.org/relation/14071495) |
