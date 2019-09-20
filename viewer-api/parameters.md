# Parameters

To control Viewer’s looks and behavior a set of initialization parameters is available. They can be set both for the iframe and web component.

Example: Setting viewer parameters using web component

```html
<vctr-viewer 
    model="d6c1f27d-6a27-4c7e-bd7d-bd19d7faa56c" 
    autoplay="0" 
    turntable="0.5" 
    enableApi="1"
>
</vctr-viewer>
```

Example: Setting init parameters using iframe

```html
<iframe 
    src="https://www.vectary.com/embed/viewer/v1/?model=d6c1f27d-6a27-4c7e-bd7d-bd19d7faa56c&autoplay=0&turntable=0.5&enableApi=1" 
    frameborder="0" 
    width="100%" 
    height="480"
>
</iframe>
```


## model (string)
The only mandatory parameter for the viewer to load. It specifies the Vectary project UUID, e.g. `“d6c1f27d-6a27-4c7e-bd7d-bd19d7faa56c"`. To load the project in Viewer, it first needs to be generated in the Embed panel.

## enableApi (num, default: 0)
If set to 1, the viewer can be controlled via JavaScript Viewer API calls.

## autoplay (num, default: 1)
If set to 0, viewer will show a play button and a static scene thumbnail in the background. This is useful if you want the user to control when the viewer loads.

> See the [live demo](https://codepen.io/vectary/pen/zYOpJyZ?editors=1000)

## showPreloader (num, default: 1)
If set to 0, viewer will hide the preloader animation and loading progress.

## turntable (num, default: 0)
If not set to 0, it will automatically rotate the scene. The value represents speed in Revolutions per minute (RPM). Negative value sets speed in counter-clockwise direction.

> See the [live demo](https://codepen.io/vectary/pen/LYPeJaQ?editors=1000)

## gestureHandling (string, default: inferior) 
Controls the scrolling behavior of Viewer. Allowed values:
- `gestureHandling=“superior"` - scene can be zoomed by scrolling the mouse over the scene.
- `gestureHandling=“inferior"` (default) - forces user to hold the Cmd (Mac) or Ctrl (PC) for zooming with mouse scroll. This option is useful when loading the viewer in fullscreen.

## showGesturePrompts (num, default: 1) 
If set to 0, no prompts instructing users on how to control the scene (e.g. using Cmd+Scroll to zoom) will be shown.

## hideMeshes (num, default: 0)
If set to 1, viewer will load with all meshes set to invisible. This is useful when you need to control visibility manually via [setVisibility](methods.md#setvisibility-name-string-visible-boolean) method.

## zoom (num, default: 1)
If set to 0, any zooming of the scene is disabled.

> See the [live demo](https://codepen.io/vectary/pen/LYPeJvQ?editors=1000)

## rotateX (num, default: 1)
If set to 0, rotation on the X axis is disabled.

> See the [live demo](https://codepen.io/vectary/pen/pozpOMy?editors=1000)

## rotateY (num, default: 1)
If set to 0, rotation on the Y axis is disabled.

> See the [live demo](https://codepen.io/vectary/pen/pozpOMy?editors=1000)

## panX (num, default: 1)
If set to 0, panning on the X axis is disabled

> See the [live demo](https://codepen.io/vectary/pen/YzKYOmO?editors=1000)

## panY (num, default: 1)
If set to 0, panning on the Y axis is disabled

> See the [live demo](https://codepen.io/vectary/pen/YzKYOmO?editors=1000)

## zoomIn (num, default: 100)
Value represents the percentage of possible zooming in. 0 means no zoom in, 100 means full zoom in. Note: this setting will be applied to all cameras on scene. Allowed values: 0 - 100.

> See the [live demo](https://codepen.io/vectary/pen/VwZydNo?editors=1000)

## zoomOut (num, default: Infinity)
Value represents the percentage of possible zooming out. 0 means no zoom out, infinity means no limit. Note: this setting will be applied to all cameras on scene. Allowed values: 0 - infinity.

> See the [live demo](https://codepen.io/vectary/pen/VwZydNo?editors=1000)

## minAzimuth (num, default: -Infinity)
Value represents the minimal angle to which the horizontal rotation is possible. Allowed values: -Infinity - 0. @Stefan please check

> See the [live demo](https://codepen.io/vectary/pen/OJLzwLR?editors=1000)

## maxAzimuth (num, default: Infinity)
Value represents the maximum angle to which the horizontal rotation is possible. Allowed values: 0 - Infinity. @Stefan please check

> See the [live demo](https://codepen.io/vectary/pen/OJLzwLR?editors=1000)

## minPolar (num, default: 0) 
Value represents the minimal angle to which the vertical rotation is possible. Allowed values: -360 - 0. @Stefan please check

> See the [live demo](https://codepen.io/vectary/pen/VwZyBww?editors=1000)

## maxPolar (num, default: 360)
Value represents the maximum angle to which the vertical rotation is possible. Allowed values: 0 - 360. @Stefan please check

> See the [live demo](https://codepen.io/vectary/pen/VwZyBww?editors=1000)

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
Gamma factor value that is used for [gamma correcting](https://en.wikipedia.org/wiki/Gamma_correction) each frame.

## baseColorGammaCorrection (num, default: 0)
Gamma correct the baseColor of each material for the factor of 2.2

## tonemap (string, default: filmic)
Tonemap setting @Stefan more info on what it is. Allowed values: 
- `linear`
- `reinhard`
- `uncharted2`
- `cineon`
- `filmic`

## exposure (num, 1.0)
Exposure value of the frame.