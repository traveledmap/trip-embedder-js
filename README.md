<p align="center">
  <a href="https://github.com/TraveledMap/trip-embedder-js">
    <img src="https://www.traveledmap.com/images/logos/traveledmap-black.png" alt="Logo" width="160">
  </a>

   <h3 align="center">TraveledMap trip itineraries embedder</h3>

  <p align="center">
    This repository contains the JavaScript library to easily display <a href="https://www.traveledmap.com">TraveledMap</a> trip itineraries maps
on a website, whatever the tool (WordPress, Prestashop, tailor made...) you're using. 🗺️ 📍
    <br />
    <br />
    <a href="https://demo.itineraries.traveledmap.com/">View Demos</a>
    ·
    <a href="https://github.com/TraveledMap/trip-embedder-js/issues">Report Bug</a>
    ·
    <a href="https://github.com/TraveledMap/trip-embedder-js/issues">Request Feature</a>
  </p>
</p>

**Before getting started**:
 - There are multiple **[demos](https://demo.itineraries.traveledmap.com/)** available: https://demo.itineraries.traveledmap.com/
 - Please remember to have a look at the [examples](#examples) and the [FAQ](#faq)
if you need help
 - Using the trip itinerary tool of TraveledMap requires a subscription, [learn more](https://www.traveledmap.com/pricing?tab=2)

Table of Contents
=================

* [Quick start](#quick-start)
* [Config](#config)
* [Examples](#examples)
* [FAQ](#faq)
* [Help](#help)


## Quick start

1. First, you need to add a tag where you want to display the map, with a custom identifier.
Optionally, you can add tags with class `traveledmap-trip-step` and `data-step` attribute to define the step's anchors.
```html
<div id="traveledmap-trip-map" />

<div class="traveledmap-trip-step" data-step="my-step-1-hash">
<div class="traveledmap-trip-step" data-step="my-step-2-hash">
```
    
2. Then include the library files to load the Javascript and CSS:
```html
<script src="https://cdn.jsdelivr.net/gh/traveledmap/trip-embedder-js@latest/dist/traveledmap-trip.min.js" />
<script src="https://cdn.jsdelivr.net/gh/traveledmap/trip-embedder-js@latest/dist/traveledmap-trip.min.css" />
```

3. Finally, instantiate the trip so that the map can display. Don't forget to use your custom id and to check the
   [configuration options](#config)
```html
<script>
    const onLoad = function() {
        new TraveledMapTrip('traveledmap-trip-map', config);
    }
    
    if (window.addEventListener) {
        window.addEventListener("load", onLoad, false);
    } else if (window.attachEvent) { // IE DOM
        window.attachEvent("onload", onLoad);
    } else {
        onLoad();
    }
</script>
```

## Config
All the following properties are accepted in the configuration.

| Property                             | Required | Default value               | Description                                                                                                                                                                                                                                                                                                                                 |
|--------------------------------------| ------ |-----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| userId                               | Yes | null                        | The identifier of your TraveledMap account, find it on the [page where you can configure the trip for sharing](https://www.traveledmap.com/share)                                                                                                                                                                                           |
| tripId                               | Yes | null                        | The identifier of the trip that you want to display, find it on the [page where you can configure the trip for sharing](https://www.traveledmap.com/share)                                                                                                                                                                                  |
| isDisabled                           | No | false                       | Disabled the trip display. The trip won't display if set to true                                                                                                                                                                                                                                                                            |
| isSticky                             | No | false                       | Allows the stick the map when user scroll, to always have it visible on the screen, wherever the user is on the page.                                                                                                                                                                                                                       |
| isExtendable                         | No | false                       | Allows the user to extend the map outside it's container to let him view it on a wider area. **Applicable only if `isSticky` is true** but remind that TraveledMap maps can be extended fullscreen natively. Works along with `shouldExtendTop`, `shouldExtendRight`, `shouldExtendBottom`, `shouldExtendLeft`. [See an example](#examples) |
| isStretchable                        | No | false                       | Allows the user to increase the height (only the height) of the map. Works along with `stretchedMapHeight`                                                                                                                                                                                                                                  |
| mapHeight                            | No | 30VH                        | Defines the initial map's height. You can pass any CSS accepted value (i.e 300px, 50VH, 50%).                                                                                                                                                                                                                                               |
| stickyMapHeight                      | No | 30VH                        | Defines the map's height when it's sticky. **Applicable only if `isSticky` is true.** You can pass any CSS accepted value (i.e 300px, 50VH, 50%).                                                                                                                                                                                           |
| stretchedMapHeight                   | No | 50VH                        | Defines the map's height when it's stretched. **Applicable only if `isStretchable` is true.** You can pass any CSS accepted value (i.e 300px, 50VH, 50%).                                                                                                                                                                                   |
| stickyMarginTop                      | No | 10                          | Defines the margin in px, between the page's top border and the top of the map, once it's getting sticky. **Applicable only if `isSticky` is true.**                                                                                                                                                                                        |
| shouldExtendToTop                    | No | false                       | Allows to extend the map to the top border of the page (the window element) when the user extends the map. **Applicable only if `isExtendable` is true.**                                                                                                                                                                                   |
| shouldExtendToRight                  | No | false                       | Allows to extend the map to the right border of the page (the window element) when the user extends the map. **Applicable only if `isExtendable` is true.**                                                                                                                                                                                 |
| shouldExtendToBottom                 | No | false                       | Allows to extend the map to the bottom border of the page (the window element) when the user extends the map. **Applicable only if `isExtendable` is true.**                                                                                                                                                                                |
| shouldExtendToLeft                   | No | false                       | Allows to extend the map to the left border of the page (the window element) when the user extends the map. **Applicable only if `isExtendable` is true.**                                                                                                                                                                                  |
| marginTop                            | No | 15                          | Defines the margin in px, between the page's top border and the map, once extended by the user. **Applicable only if `isExtendable` is true.**                                                                                                                                                                                              |
| marginRight                          | No | 15                          | Defines the margin in px, between the page's right border and the map, once extended by the user. **Applicable only if `isExtendable` is true.**                                                                                                                                                                                            |
| marginBottom                         | No | 15                          | Defines the margin in px, between the page's bottom border and the map, once extended by the user. **Applicable only if `isExtendable` is true.**                                                                                                                                                                                           |
| marginLeft                           | No | 15                          | Defines the margin in px, between the page's left border and the map, once extended by the user. **Applicable only if `isExtendable` is true.**                                                                                                                                                                                             |
| shouldShowMarkersCustomization       | No | false                       | Allows to show the steps' markers customization that has been defined on TraveledMap when creating the trip. Setting this to true will show steps' icons, color and sizes instead of numbers                                                                                                                                                |
| shouldShowPictures                   | No | true                        | Defines if the trip pictures can be viewed or not                                                                                                                                                                                                                                                                                           |
| shouldShowPicturesAtStart            | No | false                       | Defines if the trip pictures will be visible directly after the map is loaded, or if it should be visible only after a user interaction. **Applicable only if `shouldShowPictures` is true**                                                                                                                                                |
| shouldShowOnPhones                   | No | true                        | Defines if the map will be visible when the page is viewed on a screen sized like a mobile (devices with screen width under 768px excluded)                                                                                                                                                                                                 | 
| shouldShowOnTablets                  | No | true                        | Defines if the map will be visible when the page is viewed on a screen sized like a tablet (devices with screen width between 768px included and 992px excluded)                                                                                                                                                                            |
| shouldShowOnLargeScreens             | No | true                        | Defines if the map will be visible when the page is viewed on a screen sized larger than tablets (devices with screen width over 992px)                                                                                                                                                                                                     |
| shouldShowSteps                      | No | false                       | Defines if the trip's steps names are visible along with their white popup                                                                                                                                                                                                                                                                  |
| shouldShowStepsWhenExtended          | No | false                       | Defines if the trip's steps names are visible along with their white popup on the global trip overview, when the map is extended. Whatever the value, if a step is focused, its name will be visible. **Applicable only if `isExtendable` is true.**                                                                                        |
| shouldShowStepsWhenStretched         | No | false                       | Defines if the trip's steps names are visible along with their white popup on the global trip overview, when the map is stretched. Whatever the value, if a step is focused, its name will be visible. **Applicable only if `isStretched` is true.**                                                                                        |
| shouldShowPicturesWhenExtended       | No | false                       | Defines if the trip's steps pictures are shown when the map is extended. **Applicable only if `isExtendable` is true.**                                                                                                                                                                                                                     |
| shouldShowPicturesWhenStretched      | No | false                       | Defines if the trip's steps pictures are shown when the map is stretched. **Applicable only if `isStretched` is true.**                                                                                                                                                                                                                     |
| isOverContent                        | No | false                       | Allows us to know if the map is overlapping the content containing the steps detail. It will allow to apply the right offset to show the next step on the map.                                                                                                                                                                              |
| shouldScrollToStepContentWhenClicked | No | true                        | Allows to disable the automatic scroll to a step's content anchor (defined through 'traveledmap-trip-step' class) when the user clicks on the corresponding map step                                                                                                                                                                        |
| baseUrl                              | No | https://www.traveledmap.com | Only for white-labeled websites, to target their TraveledMap's url.                                                                                                                                                                                                                                                                         |

## Examples
The example folder contains 4 HTML files that you can open with your browser:
 - `extendable.html` embeds a sticky map in the website's right column, that is extended outside its container, to the top,
   right and bottom of the screen.
 - `stretchable.html` embeds a sticky map in the page's text flow (representing an itinerary detail), which can be stretched
   or hidden.
 - `static.html` embeds a static map at the top of the trip itinerary's description
 - `responsive.html` embeds two sticky maps. One in the page's flow on mobile and tablet, when the 
right column isn't visible, and one in the right column on screens larger than mobiles and tablets.
   
## FAQ
<details id="find-user-id">
    <summary>Where can I find the userId?</summary>

    You can find your userId on the page that aims at sharing a trip: https://www.traveledmap.com/en/share
    Don't forget to select "Share a single trip" and "Any other tool".
</details>
<details id="find-trip-id">
    <summary>Where can I find the tripId?</summary>

    You can find your tripId on the page that aims at sharing a trip: https://www.traveledmap.com/en/share
    Don't forget to select "Share a single trip" and "Any other tool".
</details>
<details id="find-step-hash">
    <summary>Where can I find the trip steps' hash?</summary>

    You can find the hashes on the page that aims at sharing a trip: https://www.traveledmap.com/en/share
    Don't forget to select "Share a single trip" and "Any other tool".
</details>
<details id="difference-expand-stretch">
    <summary>What's the difference between expanded and stretched?</summary>

    Both expand and stretch will increase the area covered by the map, but stretch will just
    heighten (increase the height) when expand will expand outside the map's container to the
    screen limits provided in the configuration (top, right, bottom, left).
</details>

## Help
Don't hesitate to create an issue for any feature request or any bug you would find.
You can also contact us at contact@traveledmap.com
