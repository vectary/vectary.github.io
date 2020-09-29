# Types

### SceneObject
Properties:
- **name:** string
- **type:** "light" | "camera" | "mesh" | "group" | "material"
- **visible:** boolean

### Light
Properties:
- **type:** "light"
- **parentName:** string
- **parentIndex:** number

### Camera
Properties:
- **type:** "camera"
- **parentName:** string
- **parentIndex:** number

### Mesh
Properties:
- **type:** "mesh"
- **material:** string | null
- **parentName:** string
- **parentIndex:** number

### Group
Properties:
- **type:** "group"
- **parentName:** string
- **parentIndex:** number
- **childrenNames:** string[]
- **childrenIndices:** number[]

### Material
Properties:
- **name:** string
- **type:** "material"
- **visible:** boolean

### MaterialConfig

Please note video related properties are supported by web component viewer only.

Properties:
- **name:** string
- **color:** string
- **opacity:** number
- **roughness:** number
- **metalness:** number
- **map:** string
- **videoMap:** string (web component only)
- **alphaMap:** string
- **alphaVideoMap:** string (web component only)
- **aoMap:** string
- **aoVideoMap:** string (web component only)
- **aoMapIntensity:** number
- **emissive:** string
- **emissiveMap:** string
- **emissiveVideoMap:** string (web component only)
- **emissiveIntensity:** number
- **metalnessMap:** string
- **metalnessVideoMap:** string (web component only)
- **roughnessMap:** string
- **roughnessVideoMap:** string (web component only)
- **normalMap:** string
- **normalVideoMap:** string (web component only)

### AnnotationType
Properties:
- **id:** string
- **label:** string
- **name:** string
- **text:** string
- **objectName:** string
- **position:** { x: number, y: number, z: number }
- **visible:** boolean

### AnnotationConf
Properties:
- **label:** string | null
- **name:** string
- **text:** string
- **objectName:** string

### ViewState
Properties:
- **target:** number[]
- **position:** number[]
- **zoom:** number
