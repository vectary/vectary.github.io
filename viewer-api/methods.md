# Methods

!> To be able to run the API methods, enableAPI parameter needs to be enabled `enableAPI=1`.

**Using object names**

 Practically all API methods rely on object names. This makes it transparent and simple to work with, but it's good to make few things clear: 
- Object name represents the name defined in object list inside Vectary project, e.g. `Box 1` at the time time of generating the export in Vectary editor (Viewer tab). It's a good idea to organise your object list and to name them properly before generating the export for the Viewer.
- When referring to object or objects by name, make sure you are respecting case-sensitivity and replacing spaces with underscores, e.g. `Box_1`.
- Typically there are singular and plural API methods available, e.g. `getObjectByName` and `getObjectsByName`. The singular method will always return a single object, if there are multiple objects matching the name, only the first one will be returned. The plural method will always return an array of objects, if there are multiple objects matching the name, they will all be returned.
- If you rename the object in Vectary Editor and regenerate the Viewer, you also need to change the object name in your code.

**Async functions**

For better performance and user experience, we recommend using `await` before calling API methods as you can see in examples provided for each method. More information on async JavaScript functions: https://developers.google.com/web/fundamentals/primers/async-functions

**Animations**

Selected methods can be used in combination with `animate()` API helper. You can add animation to camera movements, change of materials etc. For more information see [API helpers](/helpers?id=animateduration-number-timing-function-draw-function-onfinish-function).

## General

### init()
Initialize the API.
- Input: None
- Returns: Promise<void>

```javascript
viewerApi.init();
```

> See the [live demo](https://codepen.io/vectary/pen/KKPZBgo?editors=1011)

### takeScreenshot()
Returns the current canvas view as PNG image with transparent background. Optionally, you can specify exact coordinates and size in pixels as a scissor parameter array: x starting position, y starting position, width and height.
- Input: _Optional:_ Scissor (array: [number, number, number, number]) 
- Returns: Promise<void>

```javascript
//Return whole canvas
const screenshot = await viewerApi.takeScreenshot();
//Return region of the canvas (x, y, width, height)
const screenshot = await viewerApi.takeScreenshot(100, 100, 200, 200);
```

> See the [live demo](https://codepen.io/vectary/pen/PooNNOd?editors=1011)

## Objects

### getObjects()
Returns array of all objects in the 3D scene. Available objects are Meshes, Groups, Cameras and Lights.
- Input: None
- Returns: Promise<[SceneObject](/types?id=sceneobject)[]>

```javascript
const allSceneObjects = await viewerApi.getObjects();
console.log("Objects", allSceneObjects); 
```

> See the [live demo](https://codepen.io/vectary/pen/gNRbrW?editors=1011)

### getObjectsByName()
Returns array of objects by name.
- Input: Object name (string)
- Returns: Promise<[SceneObject](/types?id=sceneobject)[]>

```javascript
const myObjects = await viewerApi.getObjectsByName("Ring");
console.log("Objects", myObjects); 
```

> See the [live demo](https://codepen.io/vectary/pen/pozdXqB?editors=1011)

### getObjectByName()
Returns single object by name.
- Input: Object name (string)
- Returns: Promise<[SceneObject](/types?id=sceneobject)>

```javascript
const myObject = await viewerApi.getObjectByName("Satellite_Antenna");
console.log("Object", myObject); 
```

> See the [live demo](https://codepen.io/vectary/pen/pozdXXm?editors=1011)

### getMeshes()
Returns array of all mesh objects in the 3D scene. 
- Input: None
- Returns: Promise<[Mesh](/types?id=mesh)[]>

```javascript
const allSceneMeshes = await viewerApi.getMeshes();
console.log("Meshes", allSceneMeshes);
```

> See the [live demo](https://codepen.io/vectary/pen/KKPZPLQ?editors=1011)

### getMeshesByName()
Returns array of mesh objects by name.
- Input: Mesh name (string)
- Returns: Promise<[Mesh](/types?id=mesh)[]> 

```javascript
const myMeshes = await viewerApi.getMeshesByName("Ring");
console.log("Meshes", myMeshes);
```

> See the [live demo](https://codepen.io/vectary/pen/zYOpYEg?editors=1011)

### getMeshByName()
Returns single mesh object by name.
- Input: Mesh name (string)
- Returns: Promise<[Mesh](/types?id=mesh)[]> 

```javascript
const myMesh = await viewerApi.getMeshByName("Satellite_Antenna");
console.log("Mesh", myMesh);
```

> See the [live demo](https://codepen.io/vectary/pen/JjPMjMd?editors=1011)

### getHitObjects()
Returns array of objects that mouse is hovering over.
- Input: None
- Returns: Promise<[SceneObject](/types?id=sceneobject)[]>
 
```javascript
const hitObjects = await viewerApi.getHitObjects();
console.log("Objects", hitObjects);
```

> See the [live demo](https://codepen.io/vectary/pen/MWgrBKX?editors=1011)

### getVisibility()
Checks current visibility of the object by name. 
- Input: Object name (string)
- Returns: Promise<boolean>

```javascript
const isVisible = await viewerApi.getVisibility("Satellite_Antenna");
console.log("Is it visible?", isVisible);
```

> See the [live demo](https://codepen.io/vectary/pen/NWKXWyz?editors=1011)

### setVisibility()
Changes visibility of the object by name. 
- Input: Object name (string), Visibility (boolean), Exclusivity (boolean)
- Returns: Promise<boolean>

```javascript
// Set Rocket group invisible
await viewerApi.setVisibility("Rocket", false, false);
// Set Rocket group visible and all other meshes invisible
await viewerApi.setVisibility("Rocket", true, true);
```

> See the [live demo](https://codepen.io/vectary/pen/qBWpBYb?editors=1011)

### getPosition()
Get the actual position (x,y,z coordinates) of the mesh or group by name.
- Input: Mesh/Group name (string)
- Returns: Promise<[number, number, number]>

```javascript
const ballPosition = await viewerApi.getPosition("Ball");
console.log("Ball position", ballPosition);
```

> See the [live demo](https://codepen.io/vectary/pen/vYBWwxq?editors=1011)

### getRotation()
Get the actual orientation of the mesh or group by name.
- Input: Mesh/Group name (string)
- Returns: Promise<[number, number, number, string]>

```javascript
const ballRotation = await viewerApi.getRotation("Ball");
console.log("Ball rotation", ballRotation);
```

> See the [live demo](https://codepen.io/vectary/pen/GRKOaYo?editors=1011)

### getScale()
Get the actual dimmensions of the mesh or group by name.
- Input: Mesh/Group name (string)
- Returns: Promise<[number, number, number]>

```javascript
const ballSize = await viewerApi.getScale("Ball");
console.log("Ball size", ballSize);
```

> See the [live demo](https://codepen.io/vectary/pen/wvwPLOx?editors=1011)

### setPositionRelative()
Moves the object or group specified by name, by defined values along the x, y, z axis. Position is changed relatively to its original position.
- Input: Object name (string), Position (array: [number, number, number]) 
- Returns: Promise<boolean>

```javascript
await viewerApi.setPositionRelative("Ball", [0.1, 0.1, 0.0]);
```

> See the [live demo](https://codepen.io/vectary/pen/gOYXVbK?editors=1011)

### setPositionAbsolute()
Moves the object or group specified by name, by defined values along the x, y, z axis. Position is changed to the specified position.
- Input: Object/Group name (string), Position (array: [number, number, number]) 
- Returns: Promise<boolean>

```javascript
await viewerApi.setPositionAbsolute("Ball", [0.0, 1.0, 0.0]);
```

> See the [live demo](https://codepen.io/vectary/pen/rNBYXOO?editors=1011)

### setRotationRelative()
Rotates the object or group specified by name, by the defined angles on the x, y, z axis. Order of rotation execution can be defined as order parameter - default value is XYZ (must be all capital letters). Rotation is changed relatively to its original rotation.
- Input: Object/Group name (string), Rotation (array: [number, number, number]), _Optional:_ Order (string)
- Returns: Promise<boolean>

```javascript
await viewerApi.setRotationRelative("Ball", [0, 0, 0]);
```

> See the [live demo](https://codepen.io/vectary/pen/MWgrgZV?editors=1011)

### setRotationAbsolute()
Rotates the object or group specified by name, by the defined angles on the x, y, z axis. Order of rotation execution can be defined as order parameter - default value is XYZ (must be all capital letters). Rotation is changed to the specified rotation.
- Input: Object/Group name (string), Rotation (array: [number, number, number]), _Optional:_ Order (string)
- Returns: Promise<boolean>

```javascript
await viewerApi.setRotationAbsolute("Ball", [0, 20, 20]);
```

> See the [live demo](https://codepen.io/vectary/pen/zYOpOeM?editors=1011)

### setScaleRelative()
Scales the object or group specified by name, by values on the x, y, z axis.
- Input: Object/Group name (string), Scale (array: [number, number, number])
- Returns: Promise<boolean>

```javascript
await viewerApi.setScaleRelative("Ball", [0.2, 0.2, 0.2]);
```

> See the [live demo](https://codepen.io/vectary/pen/aboEoMX?editors=1011)

### setScaleAbsolute()
Scales the object or group specified by name, to values on the x, y, z axis.
- Input: Object/Group name (string), Scale (array: [number, number, number])
- Returns: Promise<boolean>

```javascript
await viewerApi.setScaleAbsolute("Ball", [1, 2, 2]);
```

> See the [live demo](https://codepen.io/vectary/pen/NWKXKmg?editors=1011)

## Cameras

### getCameras()
Returns array of all camera objects in the 3D scene. 
- Input: None
- Returns: Promise<[Camera](/types?id=camera)[]> 

```javascript
const allSceneCameras = await viewerApi.getCameras();
console.log("Cameras", allSceneCameras);
```

> See the [live demo](https://codepen.io/vectary/pen/zYOpYMx?editors=1011)

### getCamerasByName ()
Returns array of camera objects by name.
- Input: Object name (string)
- Returns: Promise<[Camera](/types?id=camera)[]>

```javascript
const myCameras = await viewerApi.getCamerasByName("Camera");
console.log("Cameras", myCameras);
```

> See the [live demo](https://codepen.io/vectary/pen/RwbxNPQ?editors=1011)

### getCameraByName ()
Returns single camera object by name.
- Input: Object name (string)
- Returns: Promise<[Camera](/types?id=camera)>

```javascript
const myCamera = await viewerApi.getCameraByName("Camera");
console.log("Camera", myCamera);
```

> See the [live demo](https://codepen.io/vectary/pen/aboEzdm?editors=1011)

## Viewport

### switchView ()
Switch camera view.
- Input: Camera name (string)
- Returns: Promise<boolean>

```javascript
await viewerApi.switchView("front_camera");
```

> See the [live demo](https://codepen.io/vectary/pen/OJLzJMm?editors=1011)

### moveView ()
Moves the current view by the specified distance on XYZ axis.
- Input: Position (array: [number, number, number]) 
- Returns: Promise<boolean>

```javascript
//Move current camera without animation
await viewerApi.moveView([0.15, 0.2, 0]);

//Animated move of current camera by 0.15 on X axis and 0.2 on Y axis taking 1 second. 
//See Helpers section in API reference for more info.
animate(
  1000,
  function (timeFraction) {
    return Math.pow(timeFraction, 2);
  },
  function (_progress) {
    await vctrApi.moveView([0.1, 0.2, 0.3]);
  },
  function () {
    console.log("Done");
  }
);
```

> See the [live demo](https://codepen.io/vectary/pen/VwZywje?editors=1011)

### rotateView ()
Rotates the current view by specified angles on XY axis. Note that when rotating the view, its target is not preserved.
- Input: Rotation (array: [number, number]) 
- Returns: Promise<boolean>

```javascript
viewerApi.rotateView([30, 0]);
```

> See the [live demo](https://codepen.io/vectary/pen/qBWpBqE?editors=1011)

### zoomView ()
Zooms current view by the specified zoom factor.
- Input: Zoom level (number)
- Returns: Promise<boolean>

```javascript
viewerApi.zoomView(2);
```

> See the [live demo](https://codepen.io/vectary/pen/ZEzvEBV?editors=1011)

## Materials

### getMaterials()
Returns a list of all materials used in the 3D scene. 
- Input: None
- Returns: Promise<[Material](/types?id=material)[]>

```javascript
const allSceneMaterials = await viewerApi.getMaterials();
console.log("Materials", allSceneMaterials);
```

> See the [live demo](https://codepen.io/vectary/pen/oNvpgze?editors=1011)

### getMaterialsByName()
Returns array of materials by name.
- Input: Material name (string)
- Returns: Promise<[Material](/types?id=material)[]>

```javascript
const Material = await viewerApi.getMaterialsByName("Asteroid surface");
console.log("Material", Material); 
```

> See the [live demo](https://codepen.io/vectary/pen/zYOpxNK?editors=1011)

### getMaterialByName()
Returns single material by name.
- Input: Material name (string)
- Returns: Promise<[Material](/types?id=material)>

```javascript
const myMaterial = await viewerApi.getMaterialByName("Brown rock");
console.log("Material", myMaterial);
```

> See the [live demo](https://codepen.io/vectary/pen/dybJPmm?editors=1011)

### createMaterial()
Creates new material. When creating material, you can pass as many material properties as needed. Otionally you can clone existing material by passing its name, this way material will be cloned and only the specified properties will be changed.
- Input: [MaterialConfig](/types?id=materialconfig) (object), Material name (string)
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
viewerApi.createMaterial(newMaterial, "wood_1");  
```

> See the [live demo](https://codepen.io/vectary/pen/yLBpLqw?editors=1011)

### setMaterial()
Applies material to the object by name.
- Input: Object name (string), Material name (string)
- Returns: Promise<boolean>

```javascript
viewerApi.setMaterial("sphere_2", "my_new_material");
```

> See the [live demo](https://codepen.io/vectary/pen/xxKpbwR?editors=1011)

### updateMaterial()
Chamges existing material. Pass only those material properties that you wish to change.
- Input: Material name (string), Material properties (object)
- Returns: Promise<boolean>

```javascript
const updatedMaterial = {  
  color: "#42f477",  
  metalness: 0.5,
  roughness: 1.0
}
viewerApi.createMaterial("wood_1", updatedMaterial);  
```

> See the [live demo](https://codepen.io/vectary/pen/ZEzvYBb?editors=1011)

## Environment

### getBackground()
Returns scene background. Background is either path to an image or RGB color code.
- Input: None
- Returns: Promise<string | [number, number, number]>

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
viewerApi.setBackground([0, 0, 255]);
// Image
viewerApi.setBackground('space.hdr');
```

> See the [live demo](https://codepen.io/vectary/pen/bGbaNOb?editors=1011)


## Annotations

### enableAnnotations()
Globally controls visibility of annotations.
- Input: Visibility (boolean)
- Returns: Promise<boolean>

```javascript
await viewerApi.enableAnnotations(true);
```

> See the [live demo](https://codepen.io/vectary/pen/jONYKZy?editors=1011)

### addAnnotation()
Creates new annotation assigned to mesh by name. Annotation is placed to the center of object.
- Input: [AnnotationConf](/types?id=annotationconf) (object)
- Returns: Promise<[AnnotationType](/types?id=annotationtype) | null>

```javascript
const annotation = await viewerApi.addAnnotation({
    label: "1",
    name: "Handle",
    text: "This is obviously very handy",
    objectName: "Handle_-_baked"
});
```

> See the [live demo](https://codepen.io/vectary/pen/KKPZeem?editors=1011)

### getAnnotations()
Returns array of all added annotations.
- Input: None
- Returns: Promise<[AnnotationType](/types?id=annotationtype)[]>

```javascript
const annotations = await viewerApi.getAnnotations();
console.log("Annotations", annotations); 
```

> See the [live demo](https://codepen.io/vectary/pen/OJLzEwM?editors=1011)

### getAnnotationById()
Returns single annotation by its unique id.
- Input: Id (string)
- Returns: Promise<[AnnotationType](/types?id=annotationtype)>

```javascript
const annotation = await viewerApi.addAnnotation({
    label: "1",
    name: "Handle",
    text: "This is obviously very handy",
    objectName: "Handle_-_baked"
});

await viewerApi.getAnnotationById(annotation.id);
```

> See the [live demo](https://codepen.io/vectary/pen/XWrVYPq?editors=1011)

### removeAnnotationById()
Removes single annotation by its unique id.
- Input: Id (string)
- Returns: Promise<boolean>

```javascript
const annotation = await viewerApi.addAnnotation({
    label: "1",
    name: "Handle",
    text: "This is obviously very handy",
    objectName: "Handle_-_baked"
});

await viewerApi.removeAnnotationById(annotation.id);
```

> See the [live demo](https://codepen.io/vectary/pen/rNBpKqv?editors=1011)

### expandAnnotationsById()
Expands annotation's body by its unique id.
- Input: Ids (array), Expanded (boolean), Exclusivity (boolean)
- Returns: Promise<boolean>

```javascript
// Collapse all annotations except specified
const annotation = await viewerApi.addAnnotation({
    label: "1",
    name: "Handle",
    text: "This is obviously very handy",
    objectName: "Handle_-_baked"
});

await viewerApi.expandAnnotationsById(annotation.id, true, true);
```

> See the [live demo](https://codepen.io/vectary/pen/gOYoKZa?editors=1011)

## Highlighting

### highlightMeshesByName()
Highlight mesh objects by name. Highligting creates material overlay with specified color (default: "#ffff00") and intensity (default: 1).
- Input: Mesh names (array), Color (string), Intensity (number), Exclusivity (boolean)
- Returns: Promise<boolean>

```javascript
await viewerApi.highlightMeshesByName(["sphere_1", "cube", "cobe_12"], "#fcba03", 0.8, false);
```

> See the [live demo](https://codepen.io/vectary/pen/xxKpJbB?editors=1011)

### unhighlightMeshesByName()
Removes highlight from meshes.
- Input: None
- Returns: Promise<boolean>

```javascript
await viewerApi.unhighlightMeshesByName(["sphere_1", "cube", "cobe_12"]);
```

> See the [live demo](https://codepen.io/vectary/pen/WNedKQZ?editors=1011)
