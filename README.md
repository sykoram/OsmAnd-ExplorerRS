# Creating a custom OsmAnd rendering

## Setup & Developing

### First time setup

Setup Waydroid, install OsmAnd~ from F-Droid, setup OsmAnd (create `dev` profile, set as default).

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


### Practical tips

Open host shell from within a distrobox:
```
distrobox-host-exec bash
```

Mount the OsmAnd rendering directory:
```
sudo mount --bind ~/.local/share/waydroid/data/media/0/Android/data/net.osmand.plus/files/rendering waydroid_osmand_rendering
sudo chmod 777 waydroid_osmand_rendering
```


## Rendering

- Goal: multi-purpose, but hiking is important
- based on UniMap (basings/OsmAnd-custom-map-styles) and routes.addon.render.xml
- recommended: More details On
- less vibrant colors of larger areas (forests,...)
- smaller power tower icons
- hiking (+fitness+running) routes: remove cap=ROUND



## TODO
- other parts of UniMap? (buildings, random house numbers, ...)
- blue (?) parking spaces
- some roads in tunnels not shown?
- thinner more vibrant hiking routes, from larger zoom
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
- change icon priority?
- border style?


## Notes, tips, snippets
Hiding cliffs:
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

