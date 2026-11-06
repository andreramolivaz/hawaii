# Kauaʻi Match

A swipe-to-plan web app for a Kauaʻi trip, **Nov 7–11, 2026**. Swipe through 70 activities (right = yes, left = no, up = **Hōkū**, the must-dos), and the app builds a day-by-day plan around opening days, drive times, weather and sea conditions. The plan exports to your calendar (.ics) or as plain text.

Everything runs in the browser from a single file: `index.html` plus the photos in `img/`. No server, no accounts, no tracking. Choices are saved only in your own browser (localStorage).

## How to open it

- **On your computer:** download or clone the repo and open `index.html`.
- **As a website:** enable GitHub Pages (Settings → Pages → Deploy from branch → `main`, folder `/`). Pages on a private repo needs a paid GitHub plan; making the repo public would also make the trip dates and hotel names public.

## What it does

- **Swipe** cards with photo, price, duration, opening days, booking needs and a weather fit for each day of the trip.
- **List view** (list icon in the header): search and filter all activities by choice (yes / Hōkū / no / to swipe) or type (sea, adventure, nature, photo spots, culture, food, sunset, run & hike, or *photo-worthy*), and change any choice with one tap.
- **Plan:** a timeline per day with drive times, check-outs, a lunch break when there is room, booking checklist, alternatives and the activities that don’t fit (with the reason). Tap an item to pin it to another day or remove it.
- **Two people:** each person swipes on their own phone and exchanges a short code; activities you both like become a *Match* and get priority.
- **Export:** calendar file (.ics) for Google, Apple or Outlook Calendar, Google Calendar links per event, or copy as text.

## Trip frame built in

| | |
|---|---|
| Arrive | Sat 7 Nov, 11:03 at Līhuʻe (LIH) from LAX; Turo car |
| Nights 7–9 | Marjorie’s Kauai Inn, Lāwaʻi (south shore, 20 min from LIH); check-out Tue by 10:30; breakfast Mon–Sat |
| Night 10 | 1 Hotel Hanalei Bay, Princeville (north shore) |
| Depart | Wed 11 Nov, 15:04 from LIH to LAX; car back 2 h 30 before (adjustable) |

## How the planner works

1. Your yes / Hōkū picks (and your partner’s, if merged) get a priority; matches and Hōkū weigh the most.
2. Each activity has opening days, fixed sessions or time windows, a zone of the island and weather sensitivity (Nā Pali sea state, rain on trails, clear sky for stars).
3. A randomized greedy search (100 runs) places activities day by day, respecting opening hours, drive times between 10 zones, one lunch and one dinner per day, one run per day, and the start/end of each day (landing, check-outs, flight).
4. The best runs are repaired by trying to swap in what didn’t fit; the plan with the best score wins (value of picks, weather fit, less driving, not overloaded, room for lunch).

## Editing the activity database

All data lives in `index.html`, in the `ACT` array (one object per activity). Main fields:

| Field | Meaning |
|---|---|
| `id`, `t`, `op` | id, title, operator or place |
| `cat`, `zone` | category key (`CAT`) and island zone (`ZONES`, `*` = anywhere) |
| `p`, `pu`, `pp`, `grp` | price text, unit text, price per person, price per group (for the cost estimate) |
| `dur` | duration in minutes |
| `fix` / `win` / `wins` / `perDay` | fixed sessions `[[start,end]]`, an open window `[open,close]`, several windows (optionally tagged `lunch`/`dinner`), or a different place and window per day (minutes from midnight, Hawaiʻi time) |
| `days` | days it runs: `d7` … `d11` |
| `sea`, `rain`, `sky`, `pref` | weather sensitivity and preferred time (`early`, `am`) |
| `group` | only one activity per group is planned (e.g. all Nā Pali boats) |
| `book`, `st`, `stx`, `url` | needs booking, status (`ok` / `check`), status note, website |
| `ig` | photo-worthy |

Weather is in `WX`, drive times in `DM`, the trip frame in `confDays()`. Adding an activity at the end of `ACT` keeps the order of the others; changing the order or count changes the partner code format.

## Sources (checked Nov 5, 2026)

- NWS Honolulu: point forecasts, coastal waters, surf zone and forecast discussion.
- Hawaiʻi State Parks (DLNR) notices; Go Hāʻena (reservations, parking slots, shuttle); Recreation.gov (Kīlauea Point).
- Kauaʻi closures tracker by Bites Sights Flights (updated Nov 5); kauai.com farmers markets (updated Oct 31).
- The Garden Island and Princeville.com on the 1 Hotel Hanalei Bay reopening and restaurants.
- Operator websites: Makana Charters, Capt Andy’s, Holo Holo, Kauai Backcountry Adventures, Kipu Ranch, Princeville Ranch, Skydive Kauai, Smith’s, Lāwaʻi International Center, NTBG, Himalayan Academy.

After Hurricane Lowell things change quickly: re-check hours and access the day before. Prices are as published or estimates (marked ≈).

## Photo credits

Photos come from Wikimedia Commons and Flickr (found via Openverse) under Creative Commons licenses or public domain, resized and cropped. They are illustrative and may not show the exact place or operator.

| Activity | Author | License | Source |
|---|---|---|---|
| Private Nā Pali boat | Michelle Maria | CC BY 3.0 | [source](https://commons.wikimedia.org/wiki/File:Sailing_along_the_Napali_Coast_Kauai,_Hawaii_-_panoramio_(64).jpg) |
| Hanakāpīʻai Falls hike | paul (dex) bica from toronto, canada | CC BY 2.0 | [source](https://commons.wikimedia.org/wiki/File:Flickr_-_paul_bica_-_hanakapiai_falls.jpg) |
| Wailua & ʻŌpaekaʻa Falls | Sonof Marvin | CC BY 2.0 | [source](https://www.flickr.com/photos/14916700@N00/2350439741) |
| Private Zodiac into the sea caves | dronepicr | CC BY 2.0 | [source](https://commons.wikimedia.org/wiki/File:Zodiac_rafting_Boat_tour_Na_Pali_Coast_Kauai_Hawaii_(46227723482).jpg) |
| Tubing through plantation canals | rjones0856 | CC BY 2.0 | [source](https://commons.wikimedia.org/wiki/File:Mt._Waialeale.jpg) |
| Sunset at Welina Terrace | rfaulds | CC BY 2.0 | [source](https://www.flickr.com/photos/23234562@N04/2317119044) |
| Waimea Canyon | dronepicr | CC BY 2.0 | [source](https://commons.wikimedia.org/wiki/File:Waimea_Canyon_lookout_Kauai,_Hawaii_pano_(45365115955).jpg) |
| Rainbow eucalyptus at Keāhua | Thomas James Caldwell | CC BY-SA 2.0 | [source](https://www.flickr.com/photos/81643710@N00/16648324744) |
| Snorkel in the ʻAnini lagoon | Janine Sprout | CC BY-SA 4.0 | [source](https://commons.wikimedia.org/wiki/File:Anahola-Beach-Kauai-Trailblazer.jpg) |
| Chocolate farm tour & tasting | berniedup | CC BY-SA 2.0 | [source](https://www.flickr.com/photos/65695019@N07/17348751253) |
| Tandem skydive | Irhanz | CC BY-SA 4.0 | [source](https://commons.wikimedia.org/wiki/File:Parachuting_sport.jpg) |
| Limahuli Garden | Daderot. | CC BY-SA 3.0 | [source](https://commons.wikimedia.org/wiki/File:Limahuli_Garden_and_Preserve,_Kauai,_Hawaii_-_general_view.JPG) |
| Mahaʻulepu coast walk | cogdogblog | CC BY 2.0 | [source](https://commons.wikimedia.org/wiki/File:Maha%27ulepo_Beach_(8725739766).jpg) |
| Golden-hour couple photoshoot | unknown author | CC0 | [source](https://www.rawpixel.com/image/5904691/photo-image-public-domain-person-sky) |
| Sunrise run on the coastal path | dronepicr | CC BY 2.0 | [source](https://commons.wikimedia.org/wiki/File:Kealia_Beach_Kauai_Hawaii_(45554020174).jpg) |
| Milky Way under a new moon | International Gemini Observatory/NOIRLab/NSF/AURA/B. Tafreshi | CC BY 4.0 | [source](https://commons.wikimedia.org/wiki/File:The_Milky_Way_over_Gemini_North_(_MG_7918-CC).jpg) |
| Off-road at Kipu Ranch | Ken Curtis | CC BY-SA 2.0 | [source](https://www.flickr.com/photos/83609650@N00/172367654) |
| Lūʻau in Smith’s garden | Frank Kovalchek from Anchorage, Alaska, USA | CC BY 2.0 | [source](https://commons.wikimedia.org/wiki/File:Hula_dancers,_Poipu,_Kauai,_Hawaii_(4829082993).jpg) |
| Sunset at Hanalei Pier | IIP Photo Archive | CC BY 2.0 | [source](https://commons.wikimedia.org/wiki/File:Hanalei_Pier,_Kauai,_Hawaii,_U.S.A.jpg) |
| Lumahaʻi Beach lookout | Syced | CC0 | [source](https://commons.wikimedia.org/w/index.php?curid=82776330) |
| Secret Beach (Kauapea) | Hawaii Savvy | CC BY 2.0 | [source](https://www.flickr.com/photos/63399348@N05/7927926518) |
| Kīlauea Point lighthouse | Megan Nagel/USFWS – U.S. Fish and Wildlife Service Headquarters | CC BY 2.0 | [source](https://commons.wikimedia.org/wiki/File:Daniel_K._Inouye_Kilauea_Point_Lighthouse_-_Pacific_Region_(8758368868).jpg) |
| Allerton Garden | Daderot. | CC BY-SA 3.0 | [source](https://commons.wikimedia.org/wiki/File:Allerton_Garden,_Kauai,_Hawaii_-_view_into_valley.JPG) |
| Kauaʻi’s Hindu Monastery | Wayoyo | CC BY-SA 4.0 | [source](https://commons.wikimedia.org/w/index.php?curid=34040752) |
| Kayak the Wailua River | Tony Webster | CC BY 2.0 | [source](https://commons.wikimedia.org/wiki/File:Wailua_River_Kayaking_-_Kauai_-_Hawaii.jpg) |
| Poke and shave ice in Waimea | photoskate | CC BY 2.0 | [source](https://www.flickr.com/photos/44447572@N06/5442182933) |
| Sunset at Kekaha | dronepicr | CC BY 2.0 | [source](https://commons.wikimedia.org/wiki/File:Kekaha_Beach_Kauai_Hawaii_(31339136717).jpg) |
| Waiʻoli Huiʻia, the green church | Sharon Hahn Darlin | CC BY 2.0 | [source](https://commons.wikimedia.org/w/index.php?curid=106877470) |
| Horseback at Princeville Ranch | Audreywilson | CC BY-SA 4.0 | [source](https://commons.wikimedia.org/wiki/File:Horseback_Riding_in_Oahu.jpg) |
| Sail and snorkel on the Leila | docoverachiever | CC BY 2.0 | [source](https://www.flickr.com/photos/90692748@N04/49457698783) |
| Sunday breakfast at Kalāheo Café | ewen and donabel | CC BY 2.0 | [source](https://www.flickr.com/photos/85979850@N00/3883271076) |
| Monk seals at Poʻipū | E bailey | CC BY-SA 4.0 | [source](https://commons.wikimedia.org/wiki/File:Hawaiian_monk_seal_close-up_(Neomonachus_schauinslandi).jpg) |
| Sunset at Kēʻē, the end of the road | iamkory | CC BY 2.0 | [source](https://www.flickr.com/photos/47742365@N00/8178963605) |
| Princeville Botanical Gardens | Kirt Edblom | CC BY-SA 2.0 | [source](https://www.flickr.com/photos/27190564@N02/51372758326) |
| E-bike the coastal path | Grace808 | CC BY-SA 3.0 | [source](https://commons.wikimedia.org/wiki/File:Kealia_Beach_located_along_the_Royal_Coconut_Coast_of_Kauai,_Hawaii.jpeg) |
| Farmers market | _e.t from Saratoga, USA | CC BY-SA 2.0 | [source](https://commons.wikimedia.org/wiki/File:Oahu_farmers_market.jpg) |
| 12-passenger catamaran | Brian Heimann bjheimann | CC0 | [source](https://commons.wikimedia.org/wiki/File:Napali_Coast_1_(Unsplash).jpg) |
| Menehune Fishpond lookout | Eric Tessmer, Honolulu Hawaii | CC BY 2.0 | [source](https://www.flickr.com/photos/71856730@N04/30040861843) |
| Hanapēpē and its swinging bridge | Richard N Horne | CC BY-SA 4.0 | [source](https://commons.wikimedia.org/wiki/File:The_Hanapepe_Swinging_Bridge,_Kauai,_Hawaii.jpg) |
| Glass Beach | Travis.Thurston | CC BY-SA 3.0 | [source](https://commons.wikimedia.org/wiki/File:GlassBeach.jpg) |
| Kauai Coffee estate | Humanoid one | CC BY-SA 3.0 | [source](https://commons.wikimedia.org/wiki/File:Coffee_Kauai_2.JPG) |
| Poke at Kōloa Fish Market | ShardsOfBlue | CC BY-SA 2.0 | [source](https://www.flickr.com/photos/9350569@N08/5936608990) |
| Surf lesson in Poʻipū | Robert Linsdell from St. Andrews, Canada | CC BY 2.0 | [source](https://commons.wikimedia.org/wiki/File:Poipu_Beach,_Koloa_(502736)_(16787961722).jpg) |
| Saimin at Hamura’s | arnold / inuyaki | CC BY 2.0 | [source](https://www.flickr.com/photos/58819758@N00/2207439590) |
| Moloaʻa Bay | Skrewtape | CC BY-SA 2.0 | [source](https://www.flickr.com/photos/75243940@N00/3882883943) |
| SUP or kayak on the Hanalei River | Christopher from Salem, OR, USA | CC BY-SA 2.0 | [source](https://commons.wikimedia.org/wiki/File:Wailua_River_Kayaker_Superzoom_(3293831929).jpg) |
| Run along Hanalei Bay | Hanalei_Bay_2_-_Kauai.jpg: Ralf Beier
derivative work: W Nowicki (talk) | CC BY 3.0 | [source](https://commons.wikimedia.org/wiki/File:Hanalei_Pier_Kauai.jpg) |
| Hideaways, the hidden cove | dronepicr | CC BY 2.0 | [source](https://commons.wikimedia.org/wiki/File:Coast_of_Princeville_Kauai_Hawaii_(45553788894).jpg) |
| Nā Pali sunset dinner sail | Frank Kovalchek from Anchorage, Alaska, USA | CC BY 2.0 | [source](https://commons.wikimedia.org/wiki/File:Sunset_over_the_Napali_Coast_(8034687052).jpg) |
| Lappert’s ice cream | ella.o | CC BY 2.0 | [source](https://www.flickr.com/photos/155807330@N05/44474096241) |
| Kōloa Rum tasting | Harold Litwiler, Poppy | CC BY 2.0 | [source](https://www.flickr.com/photos/116337886@N07/27940777754) |
| Spouting Horn | Ron Clausen | CC BY-SA 4.0 | [source](https://commons.wikimedia.org/wiki/File:Spouting_horn_blowhole_Kauai_Hawaii.jpg) |
| Kilauea Fish Market | grenade | CC BY 2.0 | [source](https://www.flickr.com/photos/54432200@N00/3550810582) |
| Hanalei Valley Lookout | tdlucas5000 from Lakewood Ca., United States | CC BY-SA 2.0 | [source](https://commons.wikimedia.org/wiki/File:Taro_Fields,_Hanalei,_Kauai_(9863657395).jpg) |
| Tapas dinner at Bar Acuda | khawkins04 | CC BY 2.0 | [source](https://www.flickr.com/photos/49978063@N00/6938398411) |
| Nā Pali raft + snorkel | Sheila Sund from Salem, United States | CC BY 2.0 | [source](https://commons.wikimedia.org/wiki/File:From_inside_a_sea_cave_(34576387814).jpg) |
| Riverboat to Fern Grotto | Bret Robertson | CC BY 2.0 | [source](https://commons.wikimedia.org/wiki/File:Kamokila_Hawaiian_Village,_Kauai.jpg) |
| Shave ice in Hanalei | AlaskaDave | CC BY-SA 3.0 | [source](https://commons.wikimedia.org/wiki/File:Hilo_Ice_Shave.JPG) |
| Breakfast at Hanalei Bread Co. | Ron Cogswell | CC BY 2.0 | [source](https://www.flickr.com/photos/22711505@N05/15860057881) |
| Snorkel at Kōloa Landing | dronepicr | CC BY 2.0 | [source](https://commons.wikimedia.org/wiki/File:Na_Pali_boat_tour_turtle_Kauai,_Hawaii_(45365305785).jpg) |
| Kukuiolono Park | Cheryl Marland | CC BY 2.0 | [source](https://www.flickr.com/photos/13654353@N08/13391876793) |
| Tree Tunnel and Old Kōloa | lytfyre | CC BY-SA 2.0 | [source](https://www.flickr.com/photos/7550067@N02/4303931389) |
| Dinner at Red Salt | bryce_edwards | CC BY 2.0 | [source](https://www.flickr.com/photos/98185064@N00/449191560) |
| Poke at Pono Market | Fuzzy Gerdes | CC BY 2.0 | [source](https://www.flickr.com/photos/62616836@N00/5080403782) |
| Zipline over the forest | a4gpa | CC BY-SA 2.0 | [source](https://www.flickr.com/photos/94833286@N00/5194911172) |
| Hanakāpīʻai Beach hike | Jeff Kubina | CC BY-SA 2.0 | [source](https://commons.wikimedia.org/wiki/File:Hanakapiai_Beach,_Na_Pali_Coast,_Kauai,_Hawaii.jpg) |
| Sunrise on the east side | Heath Cajandig | CC BY 2.0 | [source](https://www.flickr.com/photos/96228372@N06/25972950804) |
