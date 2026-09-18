# Timetable and fare review — 18 September 2026

The journey desk uses published references, not a live timetable or fare feed. Review dates are distinct from effective dates. Train movement and speeds remain estimates. No operational guarantee is implied by a published timetable.

## Source selection

- BTS's older [English landing page](https://www.bts.co.th/eng/service/timetable.html) still links November 2021 Green and July 2022 Gold PDFs. Prefer the current [BTS timetable interface](https://www.bts.co.th/traintime-frequency/) and the operator-hosted [Green PDF](https://www.ebm.co.th/cms-routemap/WareHouse/TimeTable/GreenLine.pdf), effective 1 January 2026.
- The operator-hosted [Gold PDF](https://www.ebm.co.th/cms-routemap/WareHouse/TimeTable/GoldLine.pdf) is effective 1 July 2023, matching the newer [BTS PDF](https://www.bts.co.th/pdf/timetable_Gold_1JUL23.pdf). This is the newest normal-service edition located during this review; do not relabel it as a 2026 timetable.
- [SRTET timetable](https://www.srtet.co.th/th/fare-timetable) is for the **Red Lines**, not Airport Rail Link. The selected-origin pages for [Rangsit](https://www.srtet.co.th/th/fare-timetable?s=12) and [Taling Chan](https://www.srtet.co.th/th/fare-timetable?s=0) establish the reverse-direction departures. Do not confuse destination arrival tables with terminal departure tables.
- [MRTA news 35401](https://www.mrta.co.th/th/news-release/35401), dated 2 June 2026, concerns **MRTA Shuttle Bus tracking**, not a railway timetable. It is excluded from rail timing calculations.
- [BEM station timetable](https://metro.bemplc.co.th/Fare-Calculation?lang=en): weekday snapshot reviewed 18 September 2026. Blue/Purple weekend model values remain from the earlier Sunday snapshot (6 September), explicitly not presented as newly verified weekend times.
- [Pink/branch PDF](https://www.ebm.co.th/cms-routemap/WareHouse/TimeTable/PinkLine.pdf): effective 1 September 2025. [Yellow PDF](https://www.ebm.co.th/cms-routemap/WareHouse/TimeTable/YellowLine.pdf): current operator-hosted reference checked on the review date.

## Changes to the animation model

- Green: January 2026 headways; full-length Sukhumvit trains use extension intervals. Additional core trains and late short workings are excluded. Silom full-route last departures remain 00:13 from National Stadium and 23:50 from Bang Wa; the 00:00 Bang Wa departure terminates at Krung Thon Buri.
- Gold: Krung Thon Buri 06:00–00:08; Khlong San 06:06–00:14. Updated weekday/weekend 8/10/15-minute interval bands. The last Khlong San departure for all Green Line connections is 23:31.
- Blue weekdays: Lak Song 05:30–23:08; Tha Phra platforms 3–4 05:43–23:14. Purple weekdays: Khlong Bang Phai 05:30–22:56; Tao Poon 06:00–23:35.
- Pink: first Min Buri terminal departure corrected to 05:27.
- Red: explicit published departures, including different peak transitions in each direction. Both directions 05:00–00:00; Light Red every 20 minutes. Source does not label a separate weekend table; this is disclosed.
- Minute-rounded station intervals, intermediate depot launches, delays, cancellations, public holidays and supplementary trains are not fully modeled. Before-06:00 headways not specified in a source remain representative assumptions. The UI identifies normal timetables versus estimated movement.

## Fare coverage

- **BTS Green:** [adult single-journey matrix](https://www.bts.co.th/files/uploads/tickets/pdf/fare_matrix_Eff.1Nov25_SJC.pdf). Extension fares effective 1 November 2025; core fares 1 January 2023. Exact station-pair lookup across Sukhumvit and Silom. The PDF includes future N6; this unopened station is not offered in the map's selector.
- **Red Lines:** [SRTET adult base-fare matrix](https://www.srtet.co.th/th/fare-information), checked 18 September. Exact station-pair lookup, including Red-to-Red transfers. Eligible-card caps, concessions and promotions are not deducted from base fares automatically.
- **Blue:** [BEM announcement, published 15 June 2026](https://metro.bemplc.co.th/Metro-News-Detail?id=40995&lang=th). Adult range **17–44 THB**, effective 3 July 2026–2 July 2028, superseding the 45 THB maximum. The UI links to BEM for exact station-pair fares instead of inventing a distance formula.
- **Gold:** **17 THB**, effective 1 January 2026, corroborated by the [Ministry of Commerce library's reproduction of the announcement](https://e-library.moc.go.th/news/detail/3962). This is identified as a government-library reproduction, not an original operator announcement. [BTS's 2026–27 package terms](https://www.bts.co.th/XtremeSavings/index.html) also specify a 17 THB Gold Line surcharge.
- Purple, Yellow, Pink and the branch: official operator links and the [MRTA fare directory](https://www.mrta.co.th/th/fares); no unverified numeric fare is shown. MRTA's image attachments could not be retrieved during this review (HTTP 403).
- Airport Rail Link: current fare and timetable not established by the supplied sources. Explicitly marked unverified; [government operator information](https://thailand.prd.go.th/en/content/category/detail/id/2078/iid/439307) is linked. SRTET's Red Line data must not be substituted.

## Verification and maintenance

Normalized tables and source snapshots are retained in the local `work/review-2026-09-18` folder. BTS's 61-by-61 and Red's 13-by-13 matrices were checked for dimensions and symmetry. Directional departures, midnight boundaries, mobile widths (320/390), tablet/desktop widths, same-station validation and dialog keyboard/focus behavior were tested. Existing geometry, train-motion and service-notice checks pass.

A review is a dated snapshot, not a scheduled refresh. Recheck official publications before updating the embedded tables. Security headers and the two map-provider runtime network allowlists remain unchanged; external reference links open separately with `noopener noreferrer`.
