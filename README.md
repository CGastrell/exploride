# exploride
explore you ide like a champ

## The idea
It's gotta be easy, like "add geoserver/mapserver root uri, get capabilities, add all layers, emit ready" easy.  
Make it a jQuery plugin.  
Maybe depend on Bootstrap, gotta resolve viewport setup.

## Roadmap

### v0.1.0
Given a simple call with a wms resource URI:
```javascript
$('selector').exploride('http://idehost.domain/geoserver/wms');
```
the `selector` should be appended with a *mapContainer* div where a Leaflet.Map is instanced. All layers retrieved from the WMS resource should be added to the map in whatever order they were on the capabilities response.

So:
  * Retrieve capabilities from the WMS resource, parse XML and store as JSON.
  * Generate a *div.exploride.mapContainer* and append it on `selector`
  * Instance a Leaflet.Map on `mapContainer`
  * Process list of layers from the `getCapabilities` response
  * Add all layers to `map`

**Considering**:
  * `mapContainer` should be able to resolve *maximazable* space. This means define or obtain width to 100%, set a minimum height but try to set to maximum height available (weird, I know, but then, all maps are)
  * Exploride should be a stateful instance, with it's setup options, but the WMS options should be kept in a *WMS* resource instance. This should help keep the Exploride instance to a minimum setup, with references to a *WMS* resource (ie: *WMS* resource instance could have 1000 layers, but Exploride only added 1 layer and that's all it needs to know)
  * *WMS* resource should get it's own stateful instance and initialization
  * Layers *could* be a multiple layer request (LAYERS=layer1,layer2,...) but that kind of request will mess with us ahead, so, for now, layers **should** be a single layer request

### v0.2.0
  * Available and added layers should be listed in a *sidebar*
  * Mentioned *sidebar* width should initially be set on a 1:4 ratio of the map width via bootstrap col-\*-\* 
  * Layers should get their own stateful instances (a layer must be instanceable with a set of options. These options should be *extractable*)

### v0.3.0
  * Sortable layers, programatically and via UI
  * Toggle layer's visibility
  * Docs for a simple (really really simple) implementation

## Main issues boggling in my head
  * layer order is a mess: when they are parsed from the `getCapabilities` request they come without a distinguishable order. There should be 2 main options: no-order and gis-wise order. Gis-wise is, from top to bottom: point, line, polygon. Which leads to the next issue
  * layer types (point/line/poly) are nowhere to be found on standard WMS. A WFS `DescribeLayer` request is needed to be able to obtain this kind of data. And, for sake of simplicity, we're not dealing with WFS yet.
  * 
