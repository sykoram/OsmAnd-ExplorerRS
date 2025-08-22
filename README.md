# Creating a custom OsmAnd rendering

## Setup & Developing

### First time setup

Setup Waydroid, install OsmAnd~ from F-Droid, setup OsmAnd: create `dev` profile, set as default, optionally add developer widgets (zoom).

To import the rendering for the first time:
```
sudo cp dev.render.xml ~/.local/share/waydroid/data/media/0/Download/dev.render.xml
```
In Waydroid, manually open the file and import it into OsmAnd.



### Developing

Overwrite rendering with a new version:
```
sudo cp dev.render.xml ~/.local/share/waydroid/data/media/0/Android/data/net.osmand.plus/files/rendering/dev.render.xml  &&  sudo pkill -x net.osmand.plus
```
Then, simply open OsmAnd again.



## Rendering

- Goal: multi-purpose, but hiking is important
- based on UniMap (basings/OsmAnd-custom-map-styles) and routes.addon.render.xml
- recommended: More details On
- less vibrant colors of larger areas (forests,...)
- smaller power tower icons
- hiking (+fitness+running) routes: remove cap=ROUND
- hide power=substation text (at least try to)
- show address/building names from zoom 16; show house numbers from zoom 18



## TODO
- blue (?) parking spaces
- some roads in tunnels not shown?
- thinner (80%?), more vibrant (a bit less transparency) hiking routes; from larger zoom even more
- smaller (hiking) routes shields, maybe from larget zoom
- sidewalks from larger zoom
- foot & cyclo paths style
- smaller text (incl. contour lines)
- via ferrata?
- more visible train
- less visible tram
- option for subway (and public transport in general?)
- mark important buildings (church, castle, school, court, hospital, shopping center, ...)
- maybe smaller icons (smaller padding? not in circle?)
- change icon priority? - TODO
    - higher priority: camping place
    - lower priority:  information board, power=substation
- border style?




## Notes, tips, snippets

### About rendering syntax:

From `default.render.xml`
```
Elements:
    <switch> :  Old convention <group>, bundles (groups) a section of <case>, <apply>, and further <switch> levels
    <case>   :  Old convention <filter>, is the analog of (if...else)
    <apply> and <apply_if> (synonym) :  Old convention <groupFilter>, specifies additional conditions/assignments to their parent filter

    - <switch> and <case> can be top level elements, <apply> cannot

<switch> element :
    1. A <switch> (or <group>, logically the same) on the top level propagates all its attributes like e.g. strokeWidth to the <case> level (unless overwritten there)
    2. If <switch> has <case> or <switch> children, it tests these in their order with (if...else), and returns "true" when/if the first test succeeds (all others are not executed any more). If one succeeds, also all <applies> are executed in their specified order.
    3. If <switch> does not have <case> or <switch>, but only <apply> children, then it should be replaced with <case> cause it doesn't make sense .
    4. All highest (top level) occurrences of <case> elements must contain tag/value attributes! A nested sequence from the top level like <switch><switch><case tag="" value=""></switch></switch> is possible, though.

<case> element :
    1. <case> works exactly like <switch> when executing its children, but the difference is it first evaluates itself.
        A DIFFERENCE vs. <switch> is that if <case> matches, it always returns "true", while for <switch> this depends on a match of one of its children.
    2. <case> is the only logical element which can return "true" on the top level. A top level <switch> must contain at least one <case>.

<apply> element :
    1. <apply> evaluates its children just like <switch>, but it always returns "true", however nothing below evaluates this return value any more.
    2. <apply> is only executed if at least one <case> applies

<order>
    ignorePolygonArea - process polygon even if it is filtered by area
    ignorePolygonAsPointArea - process polygon as point (center) even if it is filtered by area

"nameTag" is input parameter.
    This code
        <case nameTag="ref"/>
        <case nameTag="addr:flats"/>
        <apply textSize="13"/>
    applies textSize when ref OR addr:flats are contained in the map data (obf)

    nameTag="" is used to display object name from name or name:* tags
    which name or name:* tags is used depends on application language settings and system settings
    for example next statments display river name and skip the rest of data
    <case minzoom="11" tag="waterway" value="river" textOnPath="true" textMinDistance="80" textOrder="184" nameTag=""/>
    or
    <switch minzoom="11" tag="waterway" value="river" textOnPath="true" textMinDistance="80" textOrder="184">
        <case nameTag=""/>
    </switch>

    nameTag2 explanation: nameTag2 is the usual string addition
    engine_v1 (old):  nameTag + " " + nameTag2
    OpenGL engine: nameTag + " (" + nameTag2 + ")"
    for example <case nameTag="" nameTag2="lock_name"/> displays "Object name (Object lock name)" on map

default iconOrder=90

ignoreClick (default=false) filters out "non-clickable" objects for App click-on-map (applicable to text/icons)

Explanation of strokeWidth="dp:dx": dp scales with the screen dpi, dx directly specifies physical pixels.
    Scaling factors for dp:
        xxhdpi: 3.0
        xhdpi:  2.0
        hdpi:   1.5
        mdpi:   1.0
        ldpi:   0.75
    Example:
        Effective line width for "1:1" on an xxhdpi screen calculates to "1:1" = "(1*3)" + "1" = 4 px
    Remarks:
        - strokeWidth="z" is interpreted as strokeWidth="z:0"
        - Text size is measured in dp only.

RENDERING PROPERTIES: input parameters to the style
    renderingProperty Types : string, int, boolean; possibleValues comma separated possible values for int/string

RENDERING CONSTANTS AND ATTRIBUTES: values - colors, width, .. to be used in style or by program

<order>:
    Order should be between 0 and 255 (integer) 
    input layer check tag, value, point, cycle, area 
    output ! objectType point = 1, line = 2, polygon = 3 and order

<text>:
    PRIORITY Input to filter : tag, value, zoom [minzoom, maxzoom], textLength, ref, textOrder (default=100)

<point>:
    PRIORITY Input to filter : zoom [minzoom, maxzoom], tag, value

<polygon>:
    PRIORITY Input to filter : zoom [minzoom, maxzoom], tag, value

<line>:
    ?
```

### Examples

`pathEffect="8_2_4_2"` = 8px dash, 2px gap, 4px dash, 2px gap

```xml
<renderingProperty attr="hideCliffs" name="Cliffs" description="Hide cliffs" type="boolean" possibleValues="" category="hide"/>

<order>
    <switch>
        <case tag="natural" value="cliff">
            <apply_if hideCliffs="true" order="-1"/>
        </case>
    </switch>
</order>
```

```xml
<line>
    <switch>
        <case tag="highway" value="footway" color="#ff00ff" strokeWidth="2">
            <apply_if minzoom="16" pathEffect="8_2_2_2"/>
        </case>
    </switch>
</line>
```



### Development tips

Open host shell from within a distrobox:
```
distrobox-host-exec bash
```

Mount the OsmAnd rendering directory:
```
sudo mount --bind ~/.local/share/waydroid/data/media/0/Android/data/net.osmand.plus/files/rendering waydroid_osmand_rendering
sudo chmod 777 waydroid_osmand_rendering
```
