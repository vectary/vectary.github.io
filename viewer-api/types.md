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
Properties:
- **name:** string
- **color:** string
- **opacity:** number
- **roughness:** number
- **metalness:** number
- **map:** string
- **videoMap:** string
- **alphaMap:** string
- **alphaVideoMap:** string
- **aoMap:** string
- **aoVideoMap:** string
- **aoMapIntensity:** number
- **emissive:** string
- **emissiveMap:** string
- **emissiveVideoMap:** string
- **emissiveIntensity:** number
- **metalnessMap:** string
- **metalnessVideoMap:** string
- **roughnessMap:** string
- **roughnessVideoMap:** string
- **normalMap:** string
- **normalVideoMap:** string

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
