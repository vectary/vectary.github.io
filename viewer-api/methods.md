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

## Objects

### getObjects()
Returns array of all objects in the 3D scene. Available objects are Meshes, Groups, Cameras and Lights.
- Input: None
- Returns: Promise<[SceneObject](/types?id=sceneobject)[]>

```javascript
const allSceneObjects = await viewerApi.getObjects();
console.log("Objects", allSceneObjects); 
```

### getObjectsByName()
Returns array of objects by name.
- Input: Object name (string)
- Returns: Promise<[SceneObject](/types?id=sceneobject)[]>

```javascript
const myObjects = await viewerApi.getObjectsByName("Sphere");
console.log("Objects", myObjects); 
```

### getObjectByName()
Returns single object by name.
- Input: Object name (string)
- Returns: Promise<[SceneObject](/types?id=sceneobject)>

```javascript
const myObject = await viewerApi.getObjectByName("Guitar_Neck_1");
console.log("Object", myObject); 
```
### getMeshes()
Returns array of all mesh objects in the 3D scene. 
- Input: None
- Returns: Promise<[Mesh](/types?id=mesh)[]>

```javascript
const allSceneMeshes = await viewerApi.getMeshes();
console.log("Meshes", allSceneMeshes); 
```

### getMeshesByName()
Returns array of mesh objects by name.
- Input: Mesh name (string)
- Returns: Promise<[Mesh](/types?id=mesh)[]> 

```javascript
const myMeshes = await viewerApi.getMeshesByName("Sphere_1");
console.log("Meshes", myMeshes);
```

### getMeshByName()
Returns single mesh object by name.
- Input: Mesh name (string)
- Returns: Promise<[Mesh](/types?id=mesh)[]> 

```javascript
const myMesh = await viewerApi.getMeshByName("Sphere_1");
console.log("Mesh", myMesh);
```

### getHitObjects()
Returns array of objects that mouse is hovering over.
- Input: None
- Returns: Promise<[SceneObject](/types?id=sceneobject)[]>
 
```javascript
const hitObjects = await viewerApi.getHitObjects();
console.log("Objects", hitObjects);
```

### getVisibility()
Checks current visibility of the object by name. 
- Input: Object name (string)
- Returns: Promise<boolean>

```javascript
const isVisible = await viewerApi.getVisibility("Hat_1");
console.log("Is Hat 1 visible?", isVisible);
```

### setVisibility()
Changes visibility of the object by name. 
- Input: Object name (string), Visibility (boolean), Exclusivity (boolean)
- Returns: Promise<boolean>

```javascript
// Set Hat 1 invisible
await viewerApi.setVisibility("Hat_1", false, false);
// Set Hat 2 visible and all other meshes invisible
await viewerApi.setVisibility("Hat_2", true, true);
```

### getPosition()
Get the actual position (x,y,z coordinates) of the mesh or group by name.
- Input: Mesh/Group name (string)
- Returns: Promise<[number, number, number]>

```javascript
const ballPosition = await viewerApi.getPosition("Ball");
console.log("Ball position", ballPosition);
```

### getRotation()
Get the actual orientation of the mesh or group by name.
- Input: Mesh/Group name (string)
- Returns: Promise<[number, number, number, string]>

```javascript
const ballRotation = await viewerApi.getRotation("Ball");
console.log("Ball rotation", ballRotation);
```

### getScale()
Get the actual dimmensions of the mesh or group by name.
- Input: Mesh/Group name (string)
- Returns: Promise<[number, number, number]>

```javascript
const ballSize = await viewerApi.getScale("Ball");
console.log("Ball size", ballSize);
```

### setPositionRelative()
Moves the object or group specified by name, by defined values along the x, y, z axis. Position is changed relatively to its original position.
- Input: Object name (string), Position (array: [number, number, number]) 
- Returns: Promise<boolean>

```javascript
await viewerApi.setPositionRelative("Ball", [0.1, 0.1, 0.0]);
```

### setPositionAbsolute()
Moves the object or group specified by name, by defined values along the x, y, z axis. Position is changed to the specified position.
- Input: Object/Group name (string), Position (array: [number, number, number]) 
- Returns: Promise<boolean>

```javascript
await viewerApi.setPositionAbsolute("Ball", [0.0, 1.0, 0.0]);
```

### setRotationRelative()
Rotates the object or group specified by name, by the defined angles on the x, y, z axis. Order of rotation execution can be defined as order parameter - default value is XYZ (must be all capital letters). Rotation is changed relatively to its original rotation.
- Input: Object/Group name (string), Rotation (array: [number, number, number]), _Optional:_ Order (string)
- Returns: Promise<boolean>

```javascript
await viewerApi.setRotationRelative("Ball", [0, 0, 0]);
```

### setRotationAbsolute()
Rotates the object or group specified by name, by the defined angles on the x, y, z axis. Order of rotation execution can be defined as order parameter - default value is XYZ (must be all capital letters). Rotation is changed to the specified rotation.
- Input: Object/Group name (string), Rotation (array: [number, number, number]), _Optional:_ Order (string)
- Returns: Promise<boolean>

```javascript
await viewerApi.setRotationAbsolute("Ball", [0, 20, 20]);
```

### setScaleRelative()
Scales the object or group specified by name, by values on the x, y, z axis.
- Input: Object/Group name (string), Scale (array: [number, number, number])
- Returns: Promise<boolean>

```javascript
await viewerApi.setScaleRelative("Ball", [0.2, 0.2, 0.2]);
```

### setScaleAbsolute()
Scales the object or group specified by name, to values on the x, y, z axis.
- Input: Object/Group name (string), Scale (array: [number, number, number])
- Returns: Promise<boolean>

```javascript
await viewerApi.setScaleAbsolute("Ball", [1, 2, 2]);
```

## Cameras

### getCameras()
Returns array of all camera objects in the 3D scene. 
- Input: None
- Returns: Promise<[Camera](/types?id=camera)[]> 

```javascript
const allSceneCameras = await viewerApi.getCameras();
console.log("Cameras", allSceneCameras);
```

### getCamerasByName ()
Returns array of camera objects by name.
- Input: Object name (string)
- Returns: Promise<[Camera](/types?id=camera)[]>

```javascript
const myCameras = await viewerApi.getCamerasByName("front_camera");
console.log("Cameras", myCameras);
```

### getCameraByName ()
Returns single camera object by name.
- Input: Object name (string)
- Returns: Promise<[Camera](/types?id=camera)>

```javascript
const myCamera = await viewerApi.getCameraByName("front_camera");
console.log("Camera", myCamera);
```

## Viewport

### switchView ()
Switch camera view.
- Input: Camera name (string)
- Returns: Promise<boolean>

```javascript
await viewerApi.switchView("front_camera");
```

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

### rotateView ()
Rotates the current view by specified angles on XY axis. Note that when rotating the view, its target is not preserved.
- Input: Rotation (array: [number, number]) 
- Returns: Promise<boolean>

```javascript
viewerApi.rotateView([30, 0]);
```

### zoomView ()
Zooms current view by the specified zoom factor.
- Input: Zoom level (number)
- Returns: Promise<boolean>

```javascript
viewerApi.zoomView(2);
```

## Materials

### getMaterials()
Returns a list of all materials used in the 3D scene. 
- Input: None
- Returns: Promise<[Material](/types?id=material)[]>

```javascript
const allSceneMaterials = await viewerApi.getMaterials();
console.log("Materials", allSceneMaterials);
```

### getMaterialsByName()
Returns array of materials by name.
- Input: Material name (string)
- Returns: Promise<[Material](/types?id=material)[]>

```javascript
const myMaterials = await viewerApi.getMaterialsByName("maple_wood_1");
console.log("Materials", myMaterials);
```

### getMaterialByName()
Returns single material by name.
- Input: Material name (string)
- Returns: Promise<[Material](/types?id=material)>

```javascript
const myMaterial = await viewerApi.getMaterialByName("maple_wood_1");
console.log("Material", myMaterial);
```

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

### setMaterial()
Applies material to the object by name.
- Input: Object name (string), Material name (string)
- Returns: Promise<boolean>

```javascript
viewerApi.setMaterial("sphere_2", "my_new_material");
```

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

## Environment

### getBackground()
Returns scene background. Background is either path to an image or RGB color code.
- Input: None
- Returns: Promise<string | [number, number, number]>

```javascript
const background = viewerApi.getBackground();
```

### setBackground() 
Sets scene background. Background is either path to an image or RGB color code.
- Input: Image path (string) or RGB color (array: [number, number, number])
- Returns: Promise<boolean>

```javascript
// RGB color
viewerApi.setBackground([0, 0, 255]);
// Image
viewerApi.setBackground('theaterBG.hdr');
```

## Annotations

### enableAnnotations()
Globally controls visibility of annotations.
- Input: Visibility (boolean)
- Returns: Promise<boolean>

```javascript
await viewerApi.enableAnnotations(true);
```

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

### getAnnotations()
Returns array of all added annotations.
- Input: None
- Returns: Promise<[AnnotationType](/types?id=annotationtype)[]>

```javascript
const annotations = await viewerApi.getAnnotations();
console.log("Annotations", annotations); 
```

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

## Highlighting

### highlightMeshesByName()
Highlight mesh objects by name. Highligting creates material overlay with specified color (default: "#ffff00") and intensity (default: 1).
- Input: Mesh names (array), Color (string), Intensity (number), Exclusivity (boolean)
- Returns: Promise<boolean>

```javascript
await viewerApi.highlightMeshesByName(["sphere_1", "cube", "cobe_12"], "#fcba03", 0.8, false);
```

### unhighlightMeshesByName()
Removes highlight from meshes.
- Input: None
- Returns: Promise<boolean>

```javascript
await viewerApi.unhighlightMeshesByName(["sphere_1", "cube", "cobe_12"]);
```