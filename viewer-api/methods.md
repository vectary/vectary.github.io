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
- Input: name (string)
- Returns: Promise<SceneObject[]>

```javascript
const myObjects = await viewerApi.getObjectsByName("Sphere");
console.log("Objects", myObjects); 
```

### getObjectByName()
Returns single object by name.
- Input: name (string)
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
- Input: name (string)
- Returns: Promise<Mesh[]> 

```javascript
const myMeshes = await viewerApi.getMeshesByName("Sphere_1");
console.log("Meshes", myMeshes);
```

### getMeshByName()
Returns single mesh object by name.
- Input: name (string)
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
- Input: name (string)
- Returns: Promise<boolean>

```javascript
const isVisible = await viewerApi.getVisibility("Hat_1");
console.log("Is Hat 1 visible?", isVisible);
```

### setVisibility()
Changes visibility of the object by name. 
- Input: name (string), visible (boolean), isExclusive (boolean)
- Returns: Promise<boolean>

```javascript
// Set Hat 1 invisible
await viewerApi.setVisibility("Hat_1", false, false);
// Set Hat 2 visible and all other meshes invisible
await viewerApi.setVisibility("Hat_2", true, true);
```

### getPosition()
Get the actual position (x,y,z coordinates) of the mesh by name.
- Input: name (string)
- Returns: Promise<[number, number, number]>

```javascript
const ballPosition = await viewerApi.getPosition("Ball");
console.log("Ball position", ballPosition);
```

### getRotation()
Get the actual orientation of the mesh by name.
- Input: name (string)
- Returns: Promise<[number, number, number, string]>

```javascript
const ballRotation = await viewerApi.getRotation("Ball");
console.log("Ball rotation", ballRotation);
```

### getScale()
Get the actual dimmensions of the mesh by name.
- Input: name (string)
- Returns: Promise<[number, number, number]>

```javascript
const ballSize = await viewerApi.getScale("Ball");
console.log("Ball size", ballSize);
```

### setPosition()
Moves the object specified by name, by defined values along the x, y, z axis. Position is changed relatively to its original position.
- Input: name (string), position: (array - [number, number, number]) 
- Returns: Promise<boolean>

```javascript
await viewerApi.setPosition("Ball", [0.1, 0.1, 0.0]);
```

### setRotation()
Rotates the object specified by name, by the defined angles on the x, y, z axis. Order of rotation execution can be defined as order parameter - default value is XYZ (must be all capital letters).
- Input: name (string), rotation (array - [number, number, number]), order (string)
- Returns: Promise<boolean>

```javascript
await viewerApi.setRotation("Ball", [30, 0, 0]);
```

### setScale()
Scales the object specified by name, by values on the x, y, z axis.
- Input: name (string), scale (array - [number, number, number])
- Returns: Promise<boolean>

```javascript
await viewerApi.setScale("Ball", [2, 2, 2]);
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

### getCamerasByName (name: string)
Returns array of camera objects by name.
- Input: name (string)
- Returns: Promise<Camera[]>

```javascript
const myCameras = await viewerApi.getCamerasByName("front_camera");
console.log("Cameras", myCameras);
```

### getCameraByName (name: string)
Returns single camera object by name.
- Input: name (string)
- Returns: Promise<Camera>

```javascript
const myCamera = await viewerApi.getCameraByName("front_camera");
console.log("Camera", myCamera);
```

### setCamera (name: string)
Enter camera view.
- Input: name (string)
- Returns: Promise<boolean>

```javascript
await viewerApi.setCamera("front_camera");
```

### moveCamera ()
Moves the current camera by the specified distance on XYZ axis.
- Input: position (array - [number, number, number]) 
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

### rotateCamera (rotation: [number, number])
Rotates the current camera by specified angles on XY axis. Note that when rotating the camera, its target is not preserved.
- Input: Array of numbers matching the angles.
- Returns: Promise<boolean>

```javascript
viewerApi.rotateCamera([30, 0]);
```

### zoomCamera (zoom: number)
Zooms current camera view for the specified zoom factor.
- Input: Number representing zoom factor.
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

### getMaterialsByName(name: string)
Returns details of the material. If there are two materials with the same name, both will be returned. 
- Input: String matching the name of the material.
- Returns: Promise<Material[]>

```javascript
const myMaterials = await viewerApi.getMaterialsByName("maple_wood_1");
console.log("Materials", myMaterials);
```

### getMaterialByName(name: string)
Returns details of the material. If there are two materials with the same name, the first will be returned. 
- Input: String matching the name of the material.
- Returns: Promise<Material>

```javascript
const myMaterial = await viewerApi.getMaterialByName("maple_wood_1");
console.log("Material", myMaterial);
```

### createMaterial(material: {[key: string]: string}, name?: string)
Creates new material to be used in your app. Any number of input object properties are allowed, no need to pass all. @Boris rephrase?
- Input: Object. [Optional] Name of the material to clone from
- Returns: Promise<Material>

```javascript
const newMaterial = {
  name: "New Material",
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
viewerApi.createMaterial(newMaterial);
```

### setMaterial(objectName: string, materialName: string)
Applies material to the object.
- Input: String matching the name of object. String matching the name of material
- Returns: Promise<boolean>

```javascript
viewerApi.setMaterial("sphere_2", "maple_wood_1");
```

## Environment

### getBackground()
Returns background image or color depending what is set as background. @Boris rephrase?
- Input: None
- Returns: Promise<string | [number, number, number]>

```javascript
const background = viewerApi.getBackground();
```

### setBackground(background: string | [number, number, number]) 
Sets scene background.
- Input: RGB color OR path to image 
- Returns: Promise<boolean>

```javascript
// RGB color
viewerApi.setBackground([0, 0, 255]);
// Image
viewerApi.setBackground('theaterBG.hdr');
```

## Annotations

### enableAnnotations() @TODO
Controls visibility of annotations.
- Input: Boolean
- Returns: 

```javascript
await viewerApi.enableAnnotations(true);
```

### addAnnotation() @TODO
Create new annotation assigned to mesh on the scene. Annotation is centered on the mesh.
- Input: None
- Returns: 

```javascript
const annotation = await viewerApi.addAnnotation({
    label: "1",
    name: "Handle",
    text: "This is obviously very handy",
    objectName: "Handle_-_baked"
});
```

### getAnnotations()
...
- Input: None
- Returns: 

```javascript
const annotations = await viewerApi.getAnnotations();
console.log("Annotations", annotations); 
```

### getAnnotationById()
...
- Input: None
- Returns: 

```javascript
await viewerApi.getAnnotationById(annotation.id);
```

### removeAnnotationById()
...
- Input: None
- Returns: 

```javascript
await viewerApi.removeAnnotationById(annotation.id);
```

## Highlighting

### highlightMeshByName()
...
- Input: None
- Returns: 

```javascript

```

### unhighlightMeshByName()
...
- Input: None
- Returns: 

```javascript

```