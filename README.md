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

- based on UniMap (basings/OsmAnd-custom-map-styles) and routes.addon.render.xml
- recommended: More details On
- less vibrant colors of larger areas (forests,...)



## TODO
- smaller power tower icons

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

