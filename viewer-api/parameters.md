# Parameters

To control Viewer’s looks and behavior a set of initialization parameters is available. They can be set both for the iframe and web component.

Example: Setting init parameters in an iframe

```html
<iframe src="https://www.vectary.com/embed/viewer/v1/viewer.html?model=ad1d5aa5-1946-41a7-a2c9-fe502596146f&enableApi=1&autoplay=0&turntable=0.5" frameborder="0" width="100%" height="480"></iframe>
```

Example: Setting init parameters in a web component

```html
<vctr-viewer model="ad1d5aa5-1946-41a7-a2c9-fe502596146f" autoplay="0" turntable=”0.5 enableApi=1”></vctr-viewer>
```

## model (string)
The only mandatory parameter for the viewer to load. It specifies the Vectary project UUID, e.g. `“ad1d5aa5-1946-41a7-a2c9-fe502596146f”`. To load the project in Viewer, it first needs to be generated in the Embed panel.

## enableApi (num, default: 0)
If set to 1, the viewer can be controlled via JavaScript Viewer API calls.

## autoplay (num, default: 1)
If set to 0, viewer will show a play button and a static scene thumbnail in the background. This is useful if you want the user to control when the viewer loads.

## showPreloader (num, default: 1)
If set to 0, viewer will hide the preloader animation and loading progress.

## turntable (num, default: 0)
If not set to 0, it will automatically rotate the scene. The value represents speed in Revolutions per minute (RPM). Negative value sets speed in counter-clockwise direction.

## gestureHandling (string, default: inferior) 
Controls the scrolling behavior of Viewer. Allowed values:
- `gestureHandling=“superior”` - scene can be zoomed by scrolling the mouse over the scene.
- `gestureHandling=“inferior”` (default) - forces user to hold the Cmd (Mac) or Ctrl (PC) for zooming with mouse scroll. This option is useful when loading the viewer in fullscreen.

## showGesturePrompts (num, default: 1) 
If set to 0, no prompts instructing users on how to control the scene (e.g. using Cmd+Scroll to zoom) will be shown.

## hideMeshes (num, default: 0)
If set to 1, viewer will load with all meshes set to invisible. This is useful when you need to control visibility manually via [setVisibility](methods.md#setvisibility-name-string-visible-boolean) method.

## zoom (num, default: 1)
If set to 0, any zooming of the scene is disabled.

## rotateX (num, default: 1)
If set to 0, rotation on the X axis is disabled.

## rotateY (num, default: 1)
If set to 0, rotation on the Y axis is disabled.

## panX (num, default: 1)
If set to 0, panning on the X axis is disabled

## panY (num, default: 1)
If set to 0, panning on the Y axis is disabled

## zoomIn (num, default: 100)
Value represents the percentage of possible zooming in. 0 means no zoom in, 100 means full zoom in. Note: this setting will be applied to all cameras on scene. Allowed values: 0 - 100.

## zoomOut (num, default: Infinity)
Value represents the percentage of possible zooming out. 0 means no zoom out, infinity means no limit. Note: this setting will be applied to all cameras on scene. Allowed values: 0 - infinity.


## minAzimuth (num, default: -Infinity)
Value represents the minimal angle to which the horizontal rotation is possible. Allowed values: -Infinity - 0. @Stefan please check

## maxAzimuth (num, default: Infinity)
Value represents the maximum angle to which the horizontal rotation is possible. Allowed values: 0 - Infinity. @Stefan please check

## minPolar (num, default: 0) 
Value represents the minimal angle to which the vertical rotation is possible. Allowed values: -360 - 0. @Stefan please check

## maxPolar (num, default: 360)
Value represents the maximum angle to which the vertical rotation is possible. Allowed values: 0 - 360. @Stefan please check

## env (string, default: piazzasanmarco) 
Environment map to be used in the scene. Environment map is not exported as part of the moel, if you want other than the default environment, it needs to be explicitly set. Preview of all available environment apps can be found in Vectary editor library, allowed parameter values are: 
- `autumncrossing`
- `autumnground`
- `cedarbridge`
- `cloudlayers`
- `cloudycliffsideroad`
- `cloudyvondelpark`
- `damroad`
- `fishhookbeach`
- `kiara9dusk`
- `konigsallee`
- `modernbuildings`
- `monkforest`
- `moonlessgolf`
- `piazzasanmarco`
- `redwall`
- `sataranightnolamps`
- `sataranightnolights`
- `skatepark`
- `skukuzagolf`
- `stonepines`
- `studio1`
- `studio2`
- `teufelsbergground1`
- `teufelsbergground2`
- `teufelsbergroof`
- `theskyisonfire`
- `tiber1`
- `tiergarten`
- `tuckerwreck`
- `venicesunrise`
- `vignaioli`
- `woods`


## gamma (num, default: 2.2)
Gamma factor value.  @Stefan more info

## tonemap (string, default: filmic)
Tonemap setting @Stefan more info on what it is. Allowed values: 
- `linear`
- `reinhard`
- `uncharted2`
- `cineon`
- `filmic`

## exposure (num, 1.0)
Tonemap exposure value. @Stefan more info on what it is.