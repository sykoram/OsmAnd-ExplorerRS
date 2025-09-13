# TODO
- hiking routes (+others?)
    - smaller text?
- buildings
    - from zoom 16 (all!)
    - no/less visible borders
- some roads in tunnels not shown?
- zoom 12 (Dolomiti)
    - smaller text for mountain ranges
    - higher priority for municipality names!
- smaller text
    - contour lines on lower zoom
- via ferrata?
- option for subway (and public transport in general?)
    - zoom 12-16?
- mark important buildings (church, castle, school, court, hospital, shopping center, ...)
- maybe smaller icons (smaller padding? not in circle?)
- change icon priority? - TODO
    - higher priority: camping place
    - lower priority:  information board, power=substation
- border style?
    - disable borders between municipalities
- man_made=cutline? (Milíčovský vrch)
- fix night mode
- no street names for residental/living_street at zoom 14
    - also for track/path/footway/cycleway?
- less vibrant "basic" green areas (grass?) -> more visible forests


## Don't know how / too much hassle
- smaller hiking route shields
    - changing textSize only resizes letter inside
    - but changing profile font size also resizes them!
    - think about generating a custom set (see https://github.com/osmandapp/OsmAnd-resources)
- hide text: MTB routes ("XC KKZ"...)
    - looks like there is no information in the data that this name belongs to a MTB route; eg. "XC KKZ" is assigned to a normal route
- possible, but probably too much code to copy (which isn't future-proof):
    - thinner roads (default: from line 9754), which would allow thinner hiking routes
    - a bit more details with moreDetailed="false" (eg. residental/living streets)
    - bridges: less visible (not thick black line)
