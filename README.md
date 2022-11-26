# gmap-custom-marker-vue

This component makes it simple to display some custom vue js reactive components on a google map.

## ⚠️ important note

This project is a plugin for [@fawmi/vue-google-maps](https://github.com/fawmi/vue-google-maps).

## Features

* Display reactive custom html into markers on google map using slot system

* Live property change allows simple interaction with coordonates and zindex of html marker element

* Google map clustering support (see demo for exemple)

* Simple positionning system for marker around the origin point

* Specific markers offset X and Y for more control about html element display

* Almost all API of the component is optional, just start with lon, lat property

## Installation

Install the package from [npm](https://www.npmjs.com/package/vue2-gmap-custom-marker):

`npm i vue2-gmap-custom-marker`

## Basic Usage

Import the component and use it in the components object.

```javascript
import GmapCustomMarker from 'vue2-gmap-custom-marker';

export default = {
  [...],
  components: {
      'gmap-custom-marker': GmapCustomMarker
  },
  [...]
}
```

Use the custom marker inside the map component. Add HTML or other Vue components inside the custom marker to be rendered on the map.

```vue
<GmapMap>
  <gmap-custom-marker :marker="marker">
    <img src="http://lorempixel.com/800/600/nature/" />
    <my-component></my-component>
  </gmap-custom-marker>
</GmapMap>

<script>
export default = {
  [...],
  data() {
    return {
      marker: {
        lat: 50.60229509638775,
        lng: 3.0247059387528408
      }
    }
  [...]
}
</script>
```

Use the `@click` event with the `.native` modifier to bind a function to the clicking of the custom marker.

```vue
<GmapMap>
  <gmap-custom-marker
    :marker="{ lat: 50.60229509638775, lng: 3.0247059387528408 }"
    @click.native="someFunction"
  >
    <img src="http://lorempixel.com/800/600/nature/" />
    <my-component></my-component>
  </gmap-custom-marker>
</GmapMap>
```

Specify the alignment of the marker with the `alignment` prop. Accepts 13 values: `top`, `bottom`, `left`, `right`, `center`, `topleft` | `lefttop`, `topright` | `righttop`, `bottomleft` | `leftbottom`, `bottomright` | `rightbottom`. Defines the alignment of the marker relative to the lat/lng specified, e.g. `bottomright` - the marker will be below and on the right of the location.

 ```vue
 <gmap-custom-marker
  :marker="marker"
  alignment="bottomright"
>
</gmap-custom-marker>
 ```

 ![custom markers on vue google map](alignment.png)

Manually specify an offset value for the marker in pixels with prop `offsetX` | `offsetY`. A positive `offsetX` moves the marker further right, and a positive `offsetY` moves the marker further down the page. Can be used with the `alignment` prop.

 ```vue
 <gmap-custom-marker
  :marker="marker"
  :offsetX="-10"
  :offsetY="17.5"
>
</gmap-custom-marker>
```

## Clusters

This component supports cluster markers and works like normal vue gmap clusters (since v5.4.3)

You can use cluster marker folowing the guide below:

* Install *marker-clusterer-plus* : `npm i --save marker-clusterer-plus`

* Use plugin cluster in you main.js or so (where vue and plugins are initialized)

```javascript
// Using Cluster requires marker-clusterer-plus to be installed.
import GmapCluster from "gmap-vue/dist/components/cluster";

// Note: the name "cluster" below is the one to use in the template tags
Vue.component("cluster", GmapCluster);
```

* Wrap your custom markers in the gmap component

```vue
<vue-gmap :center="markerCenter" :zoom="10" style="width: 100%" @click="onMapClick">
    <cluster>
        <gmap-custom-marker :marker="marker">
            <img src="https://vuejs.org/images/logo.png" />
        </gmap-custom-marker>
    </cluster>
<vue-gmap>
```

All markers into the cluster tag will be managed as a cluster automatically. That's all.

## Reference

**Prop**|**Type**|**Default**|**Description**|**Supported Values**
:-----:|:-----:|:-----:|:-----:|:-----:
`marker`|Object|`null`|Provide the latitude and longitude values that the marker should be displayed at. **Required**|Provide an Object with `lat` and `lng` properties. `{ lat: Number, lng: Number }`
`offsetX`|Number|`0`|The number of pixels to move the marker by in the x-direction. Postive values move the marker to the right|Positive or negative number.
`offsetY`|Number|`0`|The number of pixels to move the marker by in the y-direction. Postive values move the marker to down the page.|Positive or negative number.
`alignment`|String|`top`|The alignment of the marker element relative to the location it is displayed. e.g. `bottomright` - the marker will be below and on the right of the location.|`top`, `bottom`, `left`, `right`, `center`, `topleft`  `lefttop`, `topright`, `righttop`, `bottomleft`, `leftbottom`, `bottomright`, `rightbottom`
`zIndex`|Number|`50`| z-index of the marker. | Positive number.
`nuxtMode`|Boolean|true| Avoid marker displacement on navigation in Nuxt. | `true`, `false`

## Licence

[MIT](https://en.wikipedia.org/wiki/MIT_License)

## Support

If you want to support this plugin it is possible :smile: 

[![paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=UV5GR9QWPAEMS)
