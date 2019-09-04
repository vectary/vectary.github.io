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
- Returns: Promise<SceneObject[]>

```javascript
const allSceneObjects = await viewerApi.getObjects();
console.log("Objects", allSceneObjects); 
```

### getObjectsByName()
Returns array of objects by name.
- Input: Object name (string)
- Returns: Promise<SceneObject[]>

```javascript
const myObjects = await viewerApi.getObjectsByName("Sphere");
console.log("Objects", myObjects); 
```

### getObjectByName()
Returns single object by name.
- Input: Object name (string)
- Returns: Promise<SceneObject>

```javascript
const myObject = await viewerApi.getObjectByName("Guitar_Neck_1");
console.log("Object", myObject); 
```
### getMeshes()
Returns array of all mesh objects in the 3D scene. 
- Input: None
- Returns: Promise<Mesh[]>

```javascript
const allSceneMeshes = await viewerApi.getMeshes();
console.log("Meshes", allSceneMeshes); 
```

### getMeshesByName()
Returns array of mesh objects by name.
- Input: Mesh name (string)
- Returns: Promise<Mesh[]> 

```javascript
const myMeshes = await viewerApi.getMeshesByName("Sphere_1");
console.log("Meshes", myMeshes);
```

### getMeshByName()
Returns single mesh object by name.
- Input: Mesh name (string)
- Returns: Promise<Mesh[]> 

```javascript
const myMesh = await viewerApi.getMeshByName("Sphere_1");
console.log("Mesh", myMesh);
```

### getHitObjects()
Returns array of objects that mouse is hovering over.
- Input: None
- Returns: Promise<SceneObject[]>
 
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
Get the actual position (x,y,z coordinates) of the mesh by name.
- Input: Mesh name (string)
- Returns: Promise<[number, number, number]>

```javascript
const ballPosition = await viewerApi.getPosition("Ball");
console.log("Ball position", ballPosition);
```

### getRotation()
Get the actual orientation of the mesh by name.
- Input: Mesh name (string)
- Returns: Promise<[number, number, number, string]>

```javascript
const ballRotation = await viewerApi.getRotation("Ball");
console.log("Ball rotation", ballRotation);
```

### getScale()
Get the actual dimmensions of the mesh by name.
- Input: Mesh name (string)
- Returns: Promise<[number, number, number]>

```javascript
const ballSize = await viewerApi.getScale("Ball");
console.log("Ball size", ballSize);
```

### setPositionRelative()
Moves the object specified by name, by defined values along the x, y, z axis. Position is changed relatively to its original position.
- Input: Object name (string), Position (array: [number, number, number]) 
- Returns: Promise<boolean>

```javascript
await viewerApi.setPositionRelative("Ball", [0.1, 0.1, 0.0]);
```

### setPositionAbsolute()
Moves the object specified by name, by defined values along the x, y, z axis. Position is changed absolutely to its original position.
- Input: Object name (string), Position (array: [number, number, number]) 
- Returns: Promise<boolean>

```javascript
await viewerApi.setPositionAbsolute("Ball", [0.0, 1.0, 0.0]);
```

### setRotationRelative()
Rotates the object specified by name, by the defined angles on the x, y, z axis. Order of rotation execution can be defined as order parameter - default value is XYZ (must be all capital letters).
- Input: Object name (string), Rotation (array: [number, number, number]), Order (string)
- Returns: Promise<boolean>

```javascript
await viewerApi.setRotationRelative("Ball", [0, 0, 0]);
```

### setRotationAbsolute()
Rotates the object specified by name, by the defined angles on the x, y, z axis. Order of rotation execution can be defined as order parameter - default value is XYZ (must be all capital letters).
- Input: Object name (string), Rotation (array: [number, number, number]), Order (string)
- Returns: Promise<boolean>

```javascript
await viewerApi.setRotationAbsolute("Ball", [0, 20, 20]);
```

### setScaleRelative()
Scales the object specified by name, by values on the x, y, z axis.
- Input: Object name (string), Scale (array: [number, number, number])
- Returns: Promise<boolean>

```javascript
await viewerApi.setScaleRelative("Ball", [0.2, 0.2, 0.2]);
```

### setScaleAbsolute()
Scales the object specified by name, to values on the x, y, z axis.
- Input: Object name (string), Scale (array: [number, number, number])
- Returns: Promise<boolean>

```javascript
await viewerApi.setScaleAbsolute("Ball", [1, 2, 2]);
```

## Cameras

### getCameras()
Returns array of all camera objects in the 3D scene. 
- Input: None
- Returns: Promise<Camera[]> 

```javascript
const allSceneCameras = await viewerApi.getCameras();
console.log("Cameras", allSceneCameras);
```

### getCamerasByName ()
Returns array of camera objects by name.
- Input: Object name (string)
- Returns: Promise<Camera[]>

```javascript
const myCameras = await viewerApi.getCamerasByName("front_camera");
console.log("Cameras", myCameras);
```

### getCameraByName ()
Returns single camera object by name.
- Input: Object name (string)
- Returns: Promise<Camera>

```javascript
const myCamera = await viewerApi.getCameraByName("front_camera");
console.log("Camera", myCamera);
```

### setCamera ()
Enter camera view.
- Input: Camera name (string)
- Returns: Promise<boolean>

```javascript
await viewerApi.setCamera("front_camera");
```

### moveCamera ()
Moves the current camera by the specified distance on XYZ axis.
- Input: Position (array: [number, number, number]) 
- Returns: Promise<boolean>

```javascript
//Move current camera without animation
await viewerApi.moveCamera([0.15, 0.2, 0]);

//Animated move of current camera by 0.15 on X axis and 0.2 on Y axis taking 1 second. 
//See Helpers section in API reference for more info.
animate(
  1000,
  function (timeFraction) {
    return Math.pow(timeFraction, 2);
  },
  function (_progress) {
    await vctrApi.moveCamera([0.1, 0.2, 0.3]);
  },
  function () {
    console.log("Done");
  }
);
```

### rotateCamera ()
Rotates the current camera by specified angles on XY axis. Note that when rotating the camera, its target is not preserved.
- Input: Rotation (array: [number, number]) 
- Returns: Promise<boolean>

```javascript
viewerApi.rotateCamera([30, 0]);
```

### zoomCamera ()
Zooms current camera view for the specified zoom factor.
- Input: Zoom level (number)
- Returns: Promise<boolean>

```javascript
viewerApi.zoomCamera(2);
```

## Materials

### getMaterials()
Returns a list of all materials used in the 3D scene. 
- Input: None
- Returns: Promise<Material[]>

```javascript
const allSceneMaterials = await viewerApi.getMaterials();
console.log("Materials", allSceneMaterials);
```

### getMaterialsByName()
Returns array of materials by name.
- Input: Material name (string)
- Returns: Promise<Material[]>

```javascript
const myMaterials = await viewerApi.getMaterialsByName("maple_wood_1");
console.log("Materials", myMaterials);
```

### getMaterialByName()
Returns single material by name.
- Input: Material name (string)
- Returns: Promise<Material>

```javascript
const myMaterial = await viewerApi.getMaterialByName("maple_wood_1");
console.log("Material", myMaterial);
```

### createMaterial()
Creates new material. When creating material, you can pass as mmanych material properties as needed. Otionally you can clone existing material by passing its name, this way material will be cloned and only the specified properties will be changed.
- Input: Material properties (object), Material name (string)
- Returns: Promise<Material>

```javascript
const newMaterial = {
  name: "my_new_material",
  color: "#42f477",
  alphaMap: "opacity_texture.png",
  aoMap: "ao_texture.jpg",
  aoMapIntensity: 1.0,
  bumpMap: "bump_texture.png",
  bumpScale: 0.2,
  displacementMap: "displacement_texture.png",
  displacementScale: 1.0,
  displacementBias: 0.0,
  emissive: "#22f517",
  emissiveMap: "emissive_texture.jpg",
  emissiveIntensity: 0.1,
  lightMap: "lm_texture.jpg",
  lightMapIntensity: 1.0,
  map: 'diffuse_texture.jpg'
  metalness: 0.0,
  metalnessMap: "mtl_texture.png",
  normalMap: "normal_texture.jpg"
  roughnessMap: 1.0,
  roughness: 1.0,
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
- Returns: 

```javascript
await viewerApi.enableAnnotations(true);
```

### addAnnotation()
Creates new annotation assigned to mesh by name. Annotation is placed to the center of object.
- Input: annotationConf: AnnotationConf
- Returns: Promise<AnnotationType | null>

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
- Returns: Promise<AnnotationType[]>

```javascript
const annotations = await viewerApi.getAnnotations();
console.log("Annotations", annotations); 
```

### getAnnotationById()
Returns single annotation by its unique id.
- Input: Id (string)
- Returns: Promise<AnnotationType>

```javascript
await viewerApi.getAnnotationById(annotation.id);
```

### removeAnnotationById()
Removes single annotation by its unique id.
- Input: Id (string)
- Returns: Promise<boolean>

```javascript
await viewerApi.removeAnnotationById(annotation.id);
```

### expandAnnotationsById()
Controls visibility of annotation by its unique id.
- Input: Ids (array), Expanded (boolean), Exclusivity (boolean)
- Returns: Promise<boolean>

```javascript
// Make all annotations invisible except one
await viewerApi.expandAnnotationsById(annotation.id, true, true);
```

## Highlighting

### highlightMeshesByName()
Highlight mesh objects by name. Highligting creates overlay with given Color (default: "#ffff00") and Intensity (default: 1).
- Input: Mesh names (array), Color (string), Intensity (number), Exclusivity (boolean)
- Returns: Promise<boolean>

```javascript
await viewerApi.highlightMeshesByName(["sphere_1", "cube", "cobe_12"], "#fcba03", 0.8, false);
```

### unhighlightMeshesByName()
Removes highlight from mesh objects.
- Input: None
- Returns: Promise<boolean>

```javascript
await viewerApi.unhighlightMeshesByName(["sphere_1", "cube", "cobe_12"]);
```