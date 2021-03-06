# Methods

**Using object names**

Practically all API methods rely on object names. This makes it transparent and simple to work with, but it's good to make few things clear:
- Object name represents the name defined in object list inside Vectary project, e.g. `Box 1` at the time time of generating the export in Vectary editor (Viewer tab). It's a good idea to organise your object list and to name them properly before generating the export for the Viewer.
- When referring to object or objects by name, make sure you are respecting case-sensitivity and replacing spaces with underscores, e.g. `Box_1`.
- Typically there are singular and plural API methods available, e.g. `getObjectByName` and `getObjectsByName`. The singular method will always return a single object, if there are multiple objects matching the name, only the first one will be returned. The plural method will always return an array of objects, if there are multiple objects matching the name, they will all be returned.
- If you rename the object in Vectary Editor and regenerate the Viewer, you also need to change the object name in your code.

**Async functions**

For better performance and user experience, we recommend using `await` before calling API methods which return `Promises`. More information on async JavaScript functions: https://developers.google.com/web/fundamentals/primers/async-functions

**Tweening**

Some methods can be used in combination with the `animate()` API helper. You can add tweening/animation to camera movements, change of materials etc. For more information see [API helpers](/helpers.md).

You can also use external animation libraries like [GSAP](https://greensock.com/gsap/).


## General

### init()
Initialize the API.
- Input: None
- Returns: Promise<void>

```javascript
await viewerApi.init();
```

> See the [live demo](https://codepen.io/vectary/pen/KKPZBgo?editors=1011)

### load()
Loads the model if the [parameter](/parameters?id=autoload-num-default-1) `autoLoad` is set to 0.
- Input: None
- Returns: Promise<string>

```javascript
await viewerApi.load();
```

## Objects

### getObjects()
Returns array of all objects in the 3D scene. Available objects are Meshes, Groups, Cameras and Lights.
- Input: None
- Returns: [SceneObject](/types?id=sceneobject)[]

```javascript
const allSceneObjects = viewerApi.getObjects();
console.log("Objects", allSceneObjects);
```

> See the [live demo](https://codepen.io/vectary/pen/gNRbrW?editors=1011)

### getHitObjects()
Returns array of objects that mouse is hovering over.
- Input: _Optional:_ First hit only (boolean)
- Returns: [SceneObject](/types?id=sceneobject)[]

```javascript
const hitObjects = viewerApi.getHitObjects();
console.log("Objects", hitObjects);
```

> See the [live demo](https://codepen.io/vectary/pen/MWgrBKX?editors=1011)

### getObjectsByName()
Returns array of objects by name.
- Input: Object name (string)
- Returns: [SceneObject](/types?id=sceneobject)[]

```javascript
const myObjects = viewerApi.getObjectsByName("Ring");
console.log("Objects", myObjects);
```

> See the [live demo](https://codepen.io/vectary/pen/pozdXqB?editors=1011)

### getObjectByName()
Returns single object by name.
- Input: Object name (string)
- Returns: [SceneObject](/types?id=sceneobject)

```javascript
const myObject = viewerApi.getObjectByName("Satellite_Antenna");
console.log("Object", myObject);
```

> See the [live demo](https://codepen.io/vectary/pen/pozdXXm?editors=1011)

### getMeshes()
Returns array of all mesh objects in the 3D scene.
- Input: None
- Returns: [Mesh](/types?id=mesh)[]

```javascript
const allSceneMeshes = viewerApi.getMeshes();
console.log("Meshes", allSceneMeshes);
```

> See the [live demo](https://codepen.io/vectary/pen/KKPZPLQ?editors=1011)

### getMeshesByName()
Returns array of mesh objects by name.
- Input: Mesh name (string)
- Returns: [Mesh](/types?id=mesh)[]

```javascript
const myMeshes = viewerApi.getMeshesByName("Ring");
console.log("Meshes", myMeshes);
```

> See the [live demo](https://codepen.io/vectary/pen/zYOpYEg?editors=1011)

### getMeshByName()
Returns single mesh object by name.
- Input: Mesh name (string)
- Returns: [Mesh](/types?id=mesh)

```javascript
const myMesh = viewerApi.getMeshByName("Satellite_Antenna");
console.log("Mesh", myMesh);
```

> See the [live demo](https://codepen.io/vectary/pen/JjPMjMd?editors=1011)

### getVisibility()
Checks current visibility of the object by name.
- Input: Object name (string)
- Returns: boolean

```javascript
const isVisible = viewerApi.getVisibility("Satellite_Antenna");
console.log("Is it visible?", isVisible);
```

> See the [live demo](https://codepen.io/vectary/pen/NWKXWyz?editors=1011)

### setVisibility()
Changes visibility of the object by name.
- Input: Object name (string), Visibility (boolean), Exclusivity (boolean)
- Returns: boolean

```javascript
// Set Rocket group invisible
viewerApi.setVisibility("Rocket", false, false);
// Set Rocket group visible and all other meshes invisible
viewerApi.setVisibility("Rocket", true, true);
```

> See the [live demo](https://codepen.io/vectary/pen/qBWpBYb?editors=1011)

### getPosition()
Get the actual position (x,y,z coordinates) of the mesh or group by name.
- Input: Mesh/Group name (string)
- Returns: [number, number, number]

```javascript
const ballPosition = viewerApi.getPosition("Ball");
console.log("Ball position", ballPosition);
```

> See the [live demo](https://codepen.io/vectary/pen/vYBWwxq?editors=1011)

### setPositionRelative()
Moves the object or group specified by name, by defined values along the x, y, z axis. Position is changed relatively to its original position.
- Input: Object name (string), Position (array: [number, number, number])
- Returns: boolean

```javascript
viewerApi.setPositionRelative("Ball", [0.1, 0.1, 0.0]);
```

> See the [live demo](https://codepen.io/vectary/pen/gOYXVbK?editors=1011)

### setPositionAbsolute()
Moves the object or group specified by name, by defined values along the x, y, z axis. Position is changed to the specified position.
- Input: Object/Group name (string), Position (array: [number, number, number])
- Returns: boolean

```javascript
viewerApi.setPositionAbsolute("Ball", [0.0, 1.0, 0.0]);
```

> See the [live demo](https://codepen.io/vectary/pen/rNBYXOO?editors=1011)

### getRotation()
Get the actual orientation of the mesh or group by name.
- Input: Mesh/Group name (string)
- Returns: [number, number, number, string]

```javascript
const ballRotation = viewerApi.getRotation("Ball");
console.log("Ball rotation", ballRotation);
```

> See the [live demo](https://codepen.io/vectary/pen/GRKOaYo?editors=1011)

### setRotationRelative()
Rotates the object or group specified by name, by the defined angles on the x, y, z axis. Order of rotation execution can be defined as order parameter - default value is XYZ (must be all capital letters). Rotation is changed relatively to its original rotation.
- Input: Object/Group name (string), Rotation (array: [number, number, number]), _Optional:_ Order (string)
- Returns: boolean

```javascript
viewerApi.setRotationRelative("Ball", [0, 0, 0]);
```

> See the [live demo](https://codepen.io/vectary/pen/MWgrgZV?editors=1011)

### setRotationAbsolute()
Rotates the object or group specified by name, by the defined angles on the x, y, z axis. Order of rotation execution can be defined as order parameter - default value is XYZ (must be all capital letters). Rotation is changed to the specified rotation.
- Input: Object/Group name (string), Rotation (array: [number, number, number]), _Optional:_ Order (string)
- Returns: boolean

```javascript
viewerApi.setRotationAbsolute("Ball", [0, 20, 20]);
```

> See the [live demo](https://codepen.io/vectary/pen/zYOpOeM?editors=1011)

### getScale()
Get the actual dimmensions of the mesh or group by name.
- Input: Mesh/Group name (string)
- Returns: [number, number, number]

```javascript
const ballSize = viewerApi.getScale("Ball");
console.log("Ball size", ballSize);
```

> See the [live demo](https://codepen.io/vectary/pen/wvwPLOx?editors=1011)

### setScaleRelative()
Scales the object or group specified by name, by values on the x, y, z axis.
- Input: Object/Group name (string), Scale (array: [number, number, number])
- Returns: boolean

```javascript
viewerApi.setScaleRelative("Ball", [0.2, 0.2, 0.2]);
```

> See the [live demo](https://codepen.io/vectary/pen/aboEoMX?editors=1011)

### setScaleAbsolute()
Scales the object or group specified by name, to values on the x, y, z axis.
- Input: Object/Group name (string), Scale (array: [number, number, number])
- Returns: boolean

```javascript
viewerApi.setScaleAbsolute("Ball", [1, 2, 2]);
```

> See the [live demo](https://codepen.io/vectary/pen/NWKXKmg?editors=1011)

## Materials

### getMaterials()
Returns a list of all materials used in the 3D scene.
- Input: None
- Returns: [Material](/types?id=material)[]

```javascript
const allSceneMaterials = viewerApi.getMaterials();
console.log("Materials", allSceneMaterials);
```

> See the [live demo](https://codepen.io/vectary/pen/oNvpgze?editors=1011)

### getMaterialsByName()
Returns array of materials by name.
- Input: Material name (string)
- Returns: [Material](/types?id=material)[]

```javascript
const Material = viewerApi.getMaterialsByName("Asteroid surface");
console.log("Material", Material);
```

> See the [live demo](https://codepen.io/vectary/pen/zYOpxNK?editors=1011)

### getMaterialByName()
Returns single material by name.
- Input: Material name (string)
- Returns: [Material](/types?id=material)

```javascript
const myMaterial = viewerApi.getMaterialByName("Brown rock");
console.log("Material", myMaterial);
```

> See the [live demo](https://codepen.io/vectary/pen/dybJPmm?editors=1011)

### getMaterialProperties()
Returns properties of the given material.
- Input: Material name (string)
- Returns: [MaterialConfig](/types?id=materialconfig)

```javascript
const myMaterialProps = viewerApi.getMaterialProperties("Brown rock");
console.log("Material properties: ", myMaterialProps);
```

### createMaterial()
Creates new material. When creating material, you can pass as many material properties as needed. Optionally you can clone existing an material by passing its name, this way material will be cloned and only the specified properties will be changed.
- Input: Material properties ([MaterialConfig](/types?id=materialconfig)), Material name (string?)
- Returns: Promise<[Material](/types?id=material)>

```javascript
// Standard PBR example
const newMaterial = {
  name: "my_new_material";
  color?: "#42f477";
  opacity?: 1.0;
  roughness?: 1.0;
  metalness?: 0.0;
  map?: "diffuse_texture.jpg";
  alphaMap?: "opacity_texture.png";
  aoMap?: "ao_texture.jpg";
  aoMapIntensity?: 1.0;
  emissive?: "#22f517";
  emissiveMap?: "emissive_texture.jpg";
  emissiveIntensity?: 0.1;
  metalnessMap?: "mtl_texture.png";
  roughnessMap?: "roughness_texture.png";
  normalMap?: "normal_texture.png";
}
await viewerApi.createMaterial(newMaterial, "wood_1");
```

> See the [live demo](https://codepen.io/vectary/pen/yLBpLqw?editors=1011)

### updateMaterial()
Changes existing material. Pass only those material properties that you wish to change. If `withPrefetch` is set to `true` (`false` is the default), it will try to prefetch any textures in the material.
- Input: Material name (string), Material properties ([MaterialConfig](/types?id=materialconfig)), withPrefetch (boolean?: false)
- Returns: Promise<boolean>

```javascript
const updatedMaterial = {
  color: "#42f477",
  metalness: 0.5,
  roughness: 1.0
}
await viewerApi.updateMaterial("wood_1", updatedMaterial);
```

> See the [live demo](https://codepen.io/vectary/pen/ZEzvYBb?editors=1011)

### setMaterial()
Applies material to the object by name.
- Input: Object name (string), Material name (string)
- Returns: boolean

```javascript
viewerApi.setMaterial("sphere_2", "my_new_material");
```

> See the [live demo](https://codepen.io/vectary/pen/xxKpbwR?editors=1011)


## Environment

### getBackground()
Returns scene background. Background is either path to an image or RGB color code.
- Input: None
- Returns: string | [number, number, number]

```javascript
const background = viewerApi.getBackground();
```

> See the [live demo](https://codepen.io/vectary/pen/oNvpgyq?editors=1011)

### setBackground()
Sets scene background. Background is either path to an image or RGB color code.
- Input: Image path (string) or RGB color (array: [number, number, number])
- Returns: Promise<boolean>

```javascript
// RGB color
await viewerApi.setBackground([0, 0, 255]);
// Image
await viewerApi.setBackground('space.hdr');
```

> See the [live demo](https://codepen.io/vectary/pen/bGbaNOb?editors=1011)

### getExposure()
Returns the current scene exposure level.
- Input: None
- Returns: number

```javascript
const exposure = viewerApi.getExposure();
```

> See the [live demo](https://codepen.io/vectary/pen/ExaObBq?editors=1011)

### setExposure()
Sets the scene overall exposure level to specified value.
- Input: number
- Returns: boolean

```javascript
viewerApi.setExposure(1.9);
```

> See the [live demo](https://codepen.io/vectary/pen/povQdMx?editors=1011)

## Cameras & Viewport

### getCameras()
Returns array of all camera objects in the 3D scene.
- Input: None
- Returns: [Camera](/types?id=camera)[]

```javascript
const allSceneCameras = viewerApi.getCameras();
console.log("Cameras", allSceneCameras);
```

> See the [live demo](https://codepen.io/vectary/pen/zYOpYMx?editors=1011)

### getCamerasByName ()
Returns array of camera objects by name.
- Input: Object name (string)
- Returns: [Camera](/types?id=camera)[]

```javascript
const myCameras = viewerApi.getCamerasByName("Camera");
console.log("Cameras", myCameras);
```

> See the [live demo](https://codepen.io/vectary/pen/RwbxNPQ?editors=1011)

### getCameraByName ()
Returns single camera object by name.
- Input: Object name (string)
- Returns: [Camera](/types?id=camera)

```javascript
const myCamera = viewerApi.getCameraByName("Camera");
console.log("Camera", myCamera);
```

> See the [live demo](https://codepen.io/vectary/pen/aboEzdm?editors=1011)

### switchView ()
Switch camera view.
- Input: Camera name (string)
- Returns: boolean

```javascript
viewerApi.switchView("front_camera");
```

### switchViewAsync ()
Switch camera view and resolves the promise when it has finished transitioning.
- Input: Camera name (string)
- Returns: Promise<boolean>

```javascript
await viewerApi.switchViewAsync("front_camera");
```

### moveView ()
Moves the current view by the specified distance on XYZ axis.
- Input: Position (array: [number, number, number])
- Returns: boolean

```javascript
viewerApi.moveView([0.1, -0.1, 0.1]);
```

> See the [live demo](https://codepen.io/vectary/pen/VwZywje?editors=1011)

### rotateView ()
Rotates the current view by specified angles on XY axis. Note that when rotating the view, its target is not preserved.
- Input: Rotation (array: [number, number])
- Returns: boolean

```javascript
viewerApi.rotateView([30, 0]);
```

> See the [live demo](https://codepen.io/vectary/pen/qBWpBqE?editors=1011)

### zoomView ()
Zooms current view by the specified zoom factor.
- Input: Zoom level (number)
- Returns: boolean

```javascript
viewerApi.zoomView(2);
```

> See the [live demo](https://codepen.io/vectary/pen/ZEzvEBV?editors=1011)

### getFOV ()
Returns current camera field of view angle.
- Input: None
- Returns: number

```javascript
const fov = viewerApi.getFOV();
console.log("Field of view:", fov);
```

> See the [live demo](https://codepen.io/vectary/pen/LYEMVqB?editors=1011)

### setFOV ()
Sets current camera field of view angle. The angle can be netween 1 - 170.
- Input: number
- Returns: boolean

```javascript
viewerApi.setFOV(80);
```

> See the [live demo](https://codepen.io/vectary/pen/qBELdvy?editors=1011)

### getViewState()
Captures the current view state.
- Input: None
- Returns: Promise<[ViewState](/types?id=viewstate)>

```javascript
const currentState = await viewerApi.getViewState();
```

### applyViewState()
Sets the current view to a certain state.
- Input: A view state ([ViewState](/types?id=viewstate))
- Returns: boolean

```javascript
const currentState = viewerApi.getViewState();
viewerApi.applyViewState(currentState);
```

### didRenderLastFrame()
Returns true if scene was rendered last frame, false otherwise. Rendering occurs with each movement of camera, animation and mouse move. Useful for per render updates.
- Input: None
- Returns: Promise\<boolean\>

```javascript
function onAnimationFrame(timestamp) {
    vctrApi.didRenderLastFrame()
        .then((didRender) => { 
            if (didRender) {
                performPerRenderAction();
            }
        });
    window.requestAnimationFrame(onAnimationFrame);
}
window.requestAnimationFrame(onAnimationFrame);
```

## Screenshots

### takeScreenshot()
Returns the current canvas view as PNG image with transparent background. To get higher resolution of the screenshot, specify an optional Scale factor that will multiply the visible canvas pixel size (number). Optionally, you can specify exact coordinates and size in pixels as a scissor parameter array: x starting position, y starting position, width and height. In combination of both parameters, you need to manually apply custom scale to scissor parameter values.
- Input: _Optional:_ Scale (number), _Optional:_ Scissor (array: [number, number, number, number])
- Returns: string

```javascript
// Return whole canvas
const screenshot = await viewerApi.takeScreenshot();
// Return whole canvas and double the actual pixel size
const screenshot = await viewerApi.takeScreenshot(2);
// Return region of the canvas (x, y, width, height)
const screenshot = await viewerApi.takeScreenshot(1, [100, 100, 200, 200]);
```

> See the [live demo](https://codepen.io/vectary/pen/PooNNOd?editors=1011)

## Annotations

### enableAnnotations()
Globally controls visibility of annotations.
- Input: Visibility (boolean)
- Returns: boolean

```javascript
viewerApi.enableAnnotations(true);
```

> See the [live demo](https://codepen.io/vectary/pen/jONYKZy?editors=1011)

### getAnnotations()
Returns array of all added annotations.
- Input: None
- Returns: [AnnotationType](/types?id=annotationtype)[]

```javascript
const annotations = viewerApi.getAnnotations();
console.log("Annotations", annotations);
```

> See the [live demo](https://codepen.io/vectary/pen/OJLzEwM?editors=1011)

### getAnnotationById()
Returns a single annotation by its unique id.
- Input: Id (string)
- Returns: [AnnotationType](/types?id=annotationtype)

```javascript
const annotation = viewerApi.addAnnotation({
    label: "1",
    name: "Handle",
    text: "This is obviously very handy",
    objectName: "Handle_-_baked"
});

viewerApi.getAnnotationById(annotation.id);
```

> See the [live demo](https://codepen.io/vectary/pen/XWrVYPq?editors=1011)

### addAnnotation()
Creates new annotation assigned to mesh by name. Annotation is placed to the center of object.
- Input: [AnnotationConf](/types?id=annotationconf) (object)
- Returns: [AnnotationType](/types?id=annotationtype) | null

```javascript
const annotation = viewerApi.addAnnotation({
    label: "1",
    name: "Handle",
    text: "This is obviously very handy",
    objectName: "Handle_-_baked"
});
```

> See the [live demo](https://codepen.io/vectary/pen/KKPZeem?editors=1011)

### removeAnnotationById()
Removes single annotation by its unique id.
- Input: Id (string)
- Returns: boolean

```javascript
const annotation = viewerApi.addAnnotation({
    label: "1",
    name: "Handle",
    text: "This is obviously very handy",
    objectName: "Handle_-_baked"
});

viewerApi.removeAnnotationById(annotation.id);
```

> See the [live demo](https://codepen.io/vectary/pen/rNBpKqv?editors=1011)

### expandAnnotationsById()
Expands annotation's body by its unique id.
- Input: Ids (array), Expanded (boolean), Exclusivity (boolean)
- Returns: boolean

```javascript
// Collapse all annotations except specified
const annotation = viewerApi.addAnnotation({
    label: "1",
    name: "Handle",
    text: "This is obviously very handy",
    objectName: "Handle_-_baked"
});

viewerApi.expandAnnotationsById(annotation.id, true, true);
```

> See the [live demo](https://codepen.io/vectary/pen/gOYoKZa?editors=1011)

## Highlighting

### highlightMeshesByName()
Highlight mesh objects by name. Highligting creates material overlay with specified color (default: `#ffff00`) and intensity (default: 1).
- Input: Mesh names (array), Color (string), Intensity (number), Exclusivity (boolean)
- Returns: boolean

```javascript
viewerApi.highlightMeshesByName(["sphere_1", "cube", "cobe_12"], "#fcba03", 0.8, false);
```

> See the [live demo](https://codepen.io/vectary/pen/xxKpJbB?editors=1011)

### unhighlightMeshesByName()
Removes highlight from meshes.
- Input: None
- Returns: boolean

```javascript
viewerApi.unhighlightMeshesByName(["sphere_1", "cube", "cobe_12"]);
```

> See the [live demo](https://codepen.io/vectary/pen/WNedKQZ?editors=1011)

## Animations
`gltf` animations are currently WIP, if you would like to see specific functions to control them, please let us know.

### play()
Plays an animation without looping and stopping on the last frame. You can play animations in reverse by setting a negative time scale. You can even change the speed/direction while the animation is still playing, by triggering the function again with a different time scale (see the `tweening` section at the beginning of this page).
- Input: Animation Index (number), Time Scale (number)
- Returns: boolean

```javascript
let close = true;
window.addEventListener("click", e => {
    if (close) {
        console.log("closing");
        viewerApi.play(0, 1); // idxs start from 0
    }
    else {
        console.log("opening");
        viewerApi.play(0, -1); // -1 for reverse
    }
    close = !close;
});
```

## AR Badge

### setUUIDAr()
Changes the `UUID` of the project that will be loaded if the AR badge is triggered.
- Input: Model UUID (string)
- Returns: boolean

```javascript
vctrApi.setUUIDAr("d6c1f27d-6a27-4c7e-bd7d-bd19d7faa56c");
```

### triggerARClick()
Triggers the AR button emulating a click. This is specially usefull if you want to use and external button instead of the provided AR badge, or just as an additional one.
- Input: None
- Returns: boolean

```javascript
vctrApi.triggerARClick();
```
