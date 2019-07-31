# Methods

!> To be able to run the API methods, enableAPI parameter needs to be enabled `enableAPI=1`.

## General

### init() @TODO
Initialize the API.
- Input: 
- Returns: 

```javascript
viewerApi.init();
```

## Objects

### getObjects()
Gives a list of all objects in the 3D scene. Available objects are Meshes, Cameras and Lights. Groups are ignored so the objects have no hierarchy. 
- Input: None
- Returns: Promise<SceneObject[]>

```javascript
const allSceneObjects = await viewerApi.getObjects();
console.log("Objects", allSceneObjects); 
```

[Example](https://codepen.io/vectary/pen/gNRbrW?editors=1011)


### getMeshes()
Gives a list of all mesh objects in the 3D scene.
- Input: None
- Returns: Promise<Mesh[]>

```javascript
const allSceneMeshes = await viewerApi.getMeshes();
console.log("Meshes", allSceneMeshes); 
```

### getObjectsByName(name: string)
Gives details of the object. If there are two objects with the same name, both will be returned. 
- Input: String matching the name of the object. Make sure to replace spaces with underscores. @TODO
- Returns: Promise<SceneObject[]>

```javascript
const myObjects = await viewerApi.getObjectsByName("Connector");
console.log("Objects", myObjects); 
```

### getObjectByName(name: string)
Gives details of the object. If there are two objects with the same name, the first will be returned. 
- Input: String matching the name of the object. Make sure to replace spaces with underscores. @TODO
- Returns: Promise<SceneObject>

```javascript
const myObject = await viewerApi.getObjectByName("Connector");
console.log("Object", myObject); 
```

### getMeshesByName(name: string)
Gives details of the mesh object. If there are two meshes with the same name, both will be returned.
- Input: String matching the name of the mesh object.
- Returns: Promise<Mesh[]> 

```javascript
const myMeshes = await viewerApi.getMeshesByName("Sphere_1");
console.log("Meshes", myMeshes);
```

### getMeshByName(name: string)
Gives details of the mesh object. If there are two meshes with the same name, the first will be returned.
- Input: String matching the name of the mesh object.
- Returns: Promise<Mesh[]> 

```javascript
const myMesh = await viewerApi.getMeshByName("Sphere_1");
console.log("Mesh", myMesh);
```

### getHitObjects()
Gives list of objects mouse is hovering over

- Input: None
- Returns: Promise<SceneObject[]>
 
```javascript
const hitObjects = await viewerApi.getHitObjects();
console.log("Objects", hitObjects);
```

### getVisibility (name: string)
Checks initial / current? visibility of the object.
- Input: String matching the name of the object.
- Returns: Promise<boolean>

```javascript
viewerApi.getVisibility("hat_1");
```

### setVisibility (name: string, visible: boolean)
Changes visibility of the object.
- Input: String matching the name of the object. Visibility state.
- Returns: Promise<boolean>

```javascript
viewerApi.setVisibility("hat_1", false);
viewerApi.setVisibility("hat_2", true);
```

### setVisibilityExclusive(names: [string], visible: boolean, type: SceneObjectType)
Changes visibility of all object excepts the ones specified.
- Input: String array matching the names of the objects. Visibility state. Type of the scene object @Boris (here we need to add all possible scene object types)
- Returns: Promise<boolean>

```javascript
viewerApi.setVisibilityExclusive(["hat_1", "hat_2"], false, "mesh");
```

### getPosition()  @TODO
Find the actual position of mesh on the scene.
- Input: String matching the name of the mesh.
- Returns: 

```javascript

```

### getRotation() @TODO
...
- Input: String matching the name of the mesh.
- Returns: 

```javascript

```

### getScale() @TODO
...
- Input: String matching the name of the mesh.
- Returns: 

```javascript

```

### setPosition() @TODO
...
- Input: String matching the name of the mesh
- Returns: 

```javascript

```

### setRotation() @TODO
...
- Input: None
- Returns: 

```javascript

```

### setScale() @TODO
...
- Input: None
- Returns: 

```javascript

```





## Cameras

### getCameras()
Gives a list of all cameras available in the 3D scene.
- Input: None
- Returns: Promise<Camera[]> 

```javascript
const allSceneCameras = await viewerApi.getCameras();
console.log("Cameras", allSceneCameras);
```

### getCamerasByName (name: string)
Gives details of the camera. If there are two cameras with the same name, both will be returned.
- Input: String matching the name of the camera.
- Returns: Promise<Camera[]>

```javascript
const myCameras = await viewerApi.getCamerasByName("front_camera");
console.log("Cameras", myCameras);
```

### getCameraByName (name: string)
Gives details of the camera. If there are two cameras with the same name, the first will be returned.
- Input: String matching the name of the camera.
- Returns: Promise<Camera>

```javascript
const myCamera = await viewerApi.getCameraByName("front_camera");
console.log("Camera", myCamera);
```

### setCamera (name: string)
Enter camera view.
- Input: String matching the name of the camera.
- Returns: Promise<boolean>

```javascript
viewerApi.setCamera("front_camera");
```

## Materials

### getMaterials()
Gives a list of all materials used in the 3D scene. 
- Input: None
- Returns: Promise<Material[]>

```javascript
const allSceneMaterials = await viewerApi.getMaterials();
console.log("Materials", allSceneMaterials);
```

### getMaterialsByName(name: string)
Gives details of the material. If there are two materials with the same name, both will be returned. 
- Input: String matching the name of the material.
- Returns: Promise<Material[]>

```javascript
const myMaterials = await viewerApi.getMaterialsByName("maple_wood_1");
console.log("Materials", myMaterials);
```

### getMaterialByName(name: string)
Gives details of the material. If there are two materials with the same name, the first will be returned. 
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
const annotations = await vctrApi.getAnnotations();
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