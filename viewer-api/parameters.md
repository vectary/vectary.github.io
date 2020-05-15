# Parameters

To control Viewer’s looks and behavior a set of initialization parameters is available. They can be set both for the iframe and web component.

Example: Setting viewer parameters using web component

```html
<vctr-viewer
    model="d6c1f27d-6a27-4c7e-bd7d-bd19d7faa56c"
    autoplay="0"
    turntable="0.5"
>
</vctr-viewer>
```

Example: Setting init parameters using iframe in its `src` attribute

```html
<iframe
    src="https://www.vectary.com/embed/viewer/v1/?model=d6c1f27d-6a27-4c7e-bd7d-bd19d7faa56c&autoplay=0&turntable=0.5"
    frameborder="0"
    width="100%"
    height="480"
>
</iframe>
```

## Loading

### model (string)
The only mandatory parameter for the viewer to load. It specifies the Vectary project UUID, e.g. `"d6c1f27d-6a27-4c7e-bd7d-bd19d7faa56c"`. To load the project in Viewer, it first needs to be generated in the Embed panel.

### autoplay (num, default: 1)
If set to 0, viewer will show a play button and a static scene thumbnail in the background. This is useful if you want the user to control when the viewer loads.

> See the [live demo](https://codepen.io/vectary/pen/zYOpJyZ?editors=1000)

### autoLoad (num, default: 1)
If set to 0, viewer will not load until the [load](methods?id=load) method has been called. This is great for deferred loading in combination with [Intersection Observers](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API).

### loadGlb (num, default: 0)
If set to 1, viewer will attempt to load the `glb` file, available when generating files for AR in the embed pannel. For very big scenes with lots of assests and textures, this can be a good solution to speed up loading times, since the browser only requires to make one call for the binary format, instead of one call for each asset in the regular `gltf` format.

### showPreloader (num, default: 1)
If set to 0, viewer will hide the preloader spinning animation.

> See the [live demo](https://codepen.io/vectary/pen/ZEEbWep?editors=1000)

### showPlaceholder (num, default: 1)
If set to 0, viewer will hide the image placeholder during loading.

> See the [live demo](https://codepen.io/vectary/pen/WNNQwjN?editors=1000)

## Controls

### turntable (num, default: 0)
If not set to 0, it will automatically rotate the scene. The value represents speed in Revolutions per minute (RPM). Negative value sets speed in counter-clockwise direction.

> See the [live demo](https://codepen.io/vectary/pen/LYPeJaQ?editors=1000)

### mouseFollow (num, default: 0)
It can be set as a flaoting number from 0 -> 1. It indicates the rotation factor of the mouse follow. The higher the number, the more the view will rotate when hovering the mouse over the viewer. (`turntable` will override this parameter)

### showInteractionPrompt (num, default: 1)
If set to 0, viewer will not show the hand icon with left-right-left rotation 3 seconds after it's loaded, and will disable the mouse follow animation when hovering the model with the mouse. (`turntable` will override this parameter)

> See the [live demo](https://codepen.io/vectary/pen/dyooBMj?editors=1000)

### showGesturePrompts (num, default: 1)
If set to 0, no prompts instructing users on how to control the scene (e.g. using Cmd+Scroll to zoom) will be shown.

### gestureHandling (string, default: inferior)
Controls the scrolling behavior of Viewer. Allowed values:
- `gestureHandling="superior"` - scene can be zoomed by scrolling the mouse over the scene.
- `gestureHandling="inferior"` (default) - forces user to hold the Cmd (Mac) or Ctrl (PC) for zooming with mouse scroll. This option is useful when loading the viewer in fullscreen.
- `gestureHandling="none"` - disables all gestures (`rotate`, `pan` & `zoom`) except those explicitly enabled.

### rotate (num, default: 1)
If set to 0, disables rotation touch & click-drag controls.

### rotateX (num, default: 1)
If set to 0, rotation on the X axis is disabled for touch & click-drag controls.

### rotateY (num, default: 1)
If set to 0, rotation on the Y axis is disabled.

> See the [live demo](https://codepen.io/vectary/pen/pozpOMy?editors=1000)

### pan (num, default: 1)
If se to 0, panning is disabled.

### panX (num, default: 1)
If set to 0, panning on the X axis is disabled

### panY (num, default: 1)
If set to 0, panning on the Y axis is disabled

> See the [live demo](https://codepen.io/vectary/pen/YzKYOmO?editors=1000)

### zoom (num, default: 1)
If set to 0, any zooming of the scene is disabled.

### zoomIn (num, default: 100)
Value represents the percentage of possible zooming in. 0 means no zoom in, 100 means full zoom in. Note: this setting will be applied to all cameras on scene. Allowed values: 0 - 100.

### zoomOut (num, default: Infinity)
Value represents the percentage of possible zooming out. 0 means no zoom out, infinity means no limit. Note: this setting will be applied to all cameras on scene. Allowed values: 0 - infinity.

> See the [live demo](https://codepen.io/vectary/pen/VwZydNo?editors=1000)

### minAzimuth (num, default: -Infinity)
Value represents the minimal angle to which the horizontal rotation is possible. Allowed values: -Infinity - 0.

### maxAzimuth (num, default: Infinity)
Value represents the maximum angle to which the horizontal rotation is possible. Allowed values: 0 - Infinity.

> See the [live demo](https://codepen.io/vectary/pen/OJLzwLR?editors=1000)

### minPolar (num, default: 0)
Value represents the minimal angle to which the vertical rotation is possible. Allowed values: -360 - 0.

### maxPolar (num, default: 360)
Value represents the maximum angle to which the vertical rotation is possible. Allowed values: 0 - 360.

> See the [live demo](https://codepen.io/vectary/pen/VwZyBww?editors=1000)

## Rendering

### env (string, default: studio3)
Environment map to be used in the scene. Environment map is not exported as part of the moel, if you want other than the default environment, it needs to be explicitly set. Preview of all available environment apps can be found in the Vectary editor library, allowed parameter values are:
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
- `snowyforest`
- `stonepines`
- `studio1`
- `studio2`
- `studio3`
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

### tonemap (string, default: default)
[Tonemap](https://en.wikipedia.org/wiki/Tone_mapping) setting. Allowed values:
- `default` THREE.Uncharted2ToneMapping
- `linear` THREE.LinearToneMapping
- `reinhard` THREE.ReinhardToneMapping
- `cineon` THREE.CineonToneMapping
- `notone` THREE.NoToneMapping

### exposure (num, 1.0)
Exposure value of the frame.

### gamma (num, default: 2.2)
Gamma factor value that is used for [gamma correcting](https://en.wikipedia.org/wiki/Gamma_correction) each frame.

### baseColorGammaCorrection (num, default: 0)
If set to 1, gamma-corrects the baseColor of each material for the factor of 2.2

## AR Badge

### arIcon (string)
If set to absolute URL of an image file, it will replace the default AR icon in top right corner. It works best with SVG or PNG with transparent background, up to 200x50px in size.

```html
<iframe
    src="https://www.vectary.com/embed/viewer/v1/?model=d6c1f27d-6a27-4c7e-bd7d-bd19d7faa56c&arIcon=https://www.vectary.com/viewer/data/icons/noun_ar_2254890_ar_by_Sinistrad_from_the_Noun_Project.svg"
    frameborder="0"
    width="100%"
    height="480"
>
</iframe>
```

> See the [live demo](https://codepen.io/vectary/pen/GRgReVV?editors=1000)

### arX (num, default: 20)
Number of pixels that the AR badge is absolutely positioned from the `right` edge of the viewer.

### arY (num, default: 20)
Number of pixels that the AR badge is absolutely positioned from the `top` edge of the viewer.

### noAR (num, default: 0)
If set to 1, the AR badge will not be shown.

### arAndroid (string)
If set to an absolute URL of a `GLB` or `GLTF` file, it will replace the embedded AR file with the specified one. This parameter can be set as `none`, which will remove the AR icon for Android platform.

```html
<iframe
    src="https://www.vectary.com/embed/viewer/v1/?model=d6c1f27d-6a27-4c7e-bd7d-bd19d7faa56c&arAndroid=vectary.com/viewer/data/examples/cube.glb&arApple=none"
    frameborder="0"
    width="100%"
    height="480"
>
</iframe>
```

> See the [live demo](https://codepen.io/vectary/pen/qBErWEE?editors=1000)

### arApple (string)
If set to an absolute URL of an `USDZ` or `REALITY` file, it will replace the embedded AR file with the specified one. This parameter can be set as `none`, which will remove the AR icon for iOS platform.

```html
<iframe
    src="https://www.vectary.com/embed/viewer/v1/?model=d6c1f27d-6a27-4c7e-bd7d-bd19d7faa56c&arApple=https://www.vectary.com/viewer/data/examples/cube.reality&arAndroid=none"
    frameborder="0"
    width="100%"
    height="480"
>
</iframe>
```

> See the [live demo](https://codepen.io/vectary/pen/YzPZPzg?editors=1000)

### qrBackLink (number, default: 0)
If set to 1, it will append the current URL to the back of the QR generated link (Only seen in Desktop). Once a mobile phone device scans the code and proceeds to the AR experience, when exiting the AR session, it will be redirected to the said URL.

!> Using this parameter with an `iframe` will cause the redirect to point to the URL of the iframe, instead of the web page which is embeded in.
