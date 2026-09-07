# Service notices — implementation and source review

Updated 7 September 2026. The existing HTML now contains a service-notice board, status coverage for all 11 services, persistent affected-station callouts, and a source directory.

**A continuous operator disruption feed is NOT connected.** The shipped collection is deliberately empty and marked `not-connected`. No active suspension has been verified by this work. This does not establish that all services are running normally. The current UI therefore says that service status is unknown.

## Official sources found

| Services | Primary reference | Announcement channels linked by that reference |
| --- | --- | --- |
| BTS Sukhumvit, Silom, Gold | [BTS SkyTrain](https://www.bts.co.th/eng/) | [X: bts_skytrain](https://twitter.com/bts_skytrain), [Facebook: BTSSkyTrain](https://www.facebook.com/BTSSkyTrain) |
| MRT Blue, Purple | [BEM rail website](https://metro.bemplc.co.th/) | [X: bem_mrt](https://x.com/bem_mrt), [Facebook: BEM.MRT](https://www.facebook.com/BEM.MRT) |
| MRT Yellow | [EBM](https://www.ebm.co.th/) | [X: YellowLine_ebm](https://twitter.com/YellowLine_ebm), [Facebook: MRTYellowLine](https://www.facebook.com/MRTYellowLine/) |
| MRT Pink, Muang Thong Thani branch | [NBM](https://www.nbm.co.th/) | [X: MRTPinkLine](https://twitter.com/MRTPinkLine), [Facebook: MRTPinkLine](https://www.facebook.com/MRTPinkLine/) |
| Dark Red, Light Red | [SRTET](https://www.srtet.co.th/en) | [X: redlinesrtet](https://mobile.twitter.com/redlinesrtet), [Facebook: REDLineSRTET](https://www.facebook.com/REDLineSRTET/) |
| Airport Rail Link | [Department of Rail Transport](https://www.drt.go.th/) — government corroboration | The current operator alert channel could not be independently verified for integration. SRTET Red Line announcements must not be mapped to ARL. |

The operator website footer links were checked on 7 September 2026. These checks establish the identity of announcement channels; they do not establish current train status. Access to social posts was incomplete: one X channel returned 403, another supplied no readable timeline, and Facebook can require sign-in. No login, API purchase, subscription, operator contact or external publishing was performed.

The Department of Rail Transport publishes incident reports and identifies Asia Era One as ARL's operator. Its [22 July 2026 ARL incident report](https://www.drt.go.th/public-relations/ขร-ลงพื้นที่ตรวจสอบสาเห) is a historical source example, not a current alert. The report is not loaded into the map. Government reports can lag operational announcements and cannot substitute for continuous operator coverage.

The reviewed official homepages expose news and social links, but this investigation did not establish a documented, accessible, complete station-level live disruption API covering the network. This is a limit of the verified integration, not a claim that no such API exists.

## Display behavior

- Confirmed affected stations receive persistent map callouts, with an English status, station code/name, review time and official source link. They do not require hovering and remain independent of ordinary line and station-label visibility toggles. Dense or off-screen stations are also accessible from the permanent notice list's “Show affected stations” button.
- Supported effects: service suspended, service cancelled, station closed, delays and partial service. Callouts group multiple notices at the same station; station details display all of them.
- Routes and station codes are checked together. An Asok BTS alert does not automatically close the neighboring MRT Sukhumvit station. A line-wide report requires explicit line-wide scope. Pink branch scope is not inferred from the main line. Tha Phra's repeated visit uses one station marker.
- Notices use wall-clock time in Bangkok, independently of the simulation slider, pause or playback speed.
- Ten minutes is an app freshness threshold, not a promise from an operator. Overdue verification, failed loading or disappearance of an unresolved record changes it to “Update unconfirmed.” Its station marker remains until a reviewed official resumption is supplied.
- A predicted end time does not prove reopening. Explicit resolution needs its own official announcement URL and timestamp.
- Absence of a notice never produces “Normal service.” Coverage remains “Status unknown,” or the more limited “No alert in reviewed sources” after a fresh documented review.
- Trains remain a timetable-informed animation; operational notices do not turn their positions into live telemetry.

## Updating reviewed information

`service-alerts.json` next to the HTML is the map's own reviewed collection, not an operator API. An HTTP(S)-hosted page checks this file every 60 seconds with caching disabled. A successful file download updates the collection-load time, never the source-review timestamps. No server, scheduled collector, GitHub connection or Netlify deployment has been created.

When opened directly as a local file, the HTML uses its embedded snapshot. Updating an adjacent JSON file cannot update that embedded snapshot; rebuild the HTML after reviewing new information.

For a continuous live service, the remaining work is to establish authorized operator/social API access with adequate coverage, extract incident and resumption updates, verify the affected station mapping and English summary, and update this collection. The UI alone cannot perform those missing verification steps.

The source file is `work/service-alerts.json`. Validation is performed by `node work/check-alert-file.cjs`; `python3 work/build_html.py` validates it, rebuilds the HTML and copies the collection to `outputs/service-alerts.json`.

Collection fields:

| Field | Meaning |
| --- | --- |
| `schemaVersion` | `1` |
| `mode` | `not-connected` for an empty disconnected collection, or `reviewed` |
| `generatedAt` | ISO timestamp with timezone; required for reviewed collections |
| `coverage` | Reviewed route/source pairs with `providerId`, `lineId`, `checkedAt`, `result: "reviewed"` |
| `alerts` | Reviewed records, including explicit resolutions |

Each record needs `id`, `providerId`, `lineId`, `effect`, `state`, `scope`, `summaryEn`, `evidenceNote`, `verification: "human-reviewed"`, `sourceUrl`, `publishedAt`, `verifiedAt`, `startsAt` and `reviewBy`. A station-scoped record also needs explicit `stationCodes`. Optional `endsAt` records an announced expected end. Resolved records require `resolvedAt` and `resolutionUrl`. `reviewBy` must be within 10 minutes after verification.

Source URLs must be specific announcements on the allowed operator/regulator domains or posts on their verified social accounts. A homepage link is not incident evidence. The reviewer must read the announcement and confirm the English summary, affected scope and any later resumption. URL validation and the human-reviewed flag alone do not prove the contents of an external source.

## Validation performed

Automated checks cover wrong-route station codes, unverified sources, lookalike domains, invalid/future timestamps, stale reports, planned reports, expected-end behavior, explicit resolution, missing records, old collection rollback, unresolved interchanges, and repeated Tha Phra stops. DOM integration tests exercise the actual notice renderer, persistent markers with all ordinary lines hidden, separate real-world time, escaped external text, network failure and resolution removal.

Synthetic incidents are confined to the test code; the shipped collection and HTML contain none. Existing rail geometry/motion checks also pass. Visual browser verification of this revision remains incomplete because the local HTML navigation was previously rejected by the browser tool's URL security policy.
