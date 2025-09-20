# TODO
- smaller text
    - contour lines on lower zoom

- square: higher text priority
- mountain polygon color/texture from zoom 12/13
- lakes:
    - name visible from zoom 10/11/12 (maybe higher priority?)
    - gulf name more visible than lake name? (Lipno: zoom 9--12)
    - OPEN ISSUE / PR: add additional="water=lake" etc?
- hiking routes (+others?)
    - smaller text? + disable on zoom 12 (+13?)
- buildings
    - from zoom 16 (all!)
    - no/less visible borders
- some roads in tunnels not shown?
- via ferrata?
- mark important buildings (church, castle, school, court, hospital, shopping center, ...)
- maybe smaller icons (smaller padding? not in circle?)
- change icon priority? - TODO
    - higher priority: camping place
    - lower priority:  information board, power=substation
- border style - more visible between countries
- man_made=cutline? (Milíčovský vrch)
- less vibrant "basic" green areas (grass?) -> more visible forests

- improve night mode

- screenshots
- installing


## Don't know how / too much hassle
- smaller hiking route shields
    - changing textSize only resizes letter inside
    - but changing profile font size also resizes them!
    - think about generating a custom set (see https://github.com/osmandapp/OsmAnd-resources)
- hide text: MTB routes ("XC KKZ"...)
    - looks like there is no information in the data that this name belongs to a MTB route; eg. "XC KKZ" is assigned to a normal route
- possible, but probably too much code to copy (which isn't future-proof):
    - thinner roads (default: from line 9754), which would allow thinner hiking routes
    - also thicker roads for very large zoom
    - a bit more details with moreDetailed="false" (eg. residental/living streets)
    - bridges: less visible (not thick black line)
