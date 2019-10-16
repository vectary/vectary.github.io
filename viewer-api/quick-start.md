## Prepare your Embed

If you haven't done so already, head to [Vectary](https://www.vectary.com) and start new project. Create your models either by modelling from scratch or by importing from other tools or 3D libraries.

Once you're happy with your scene, you will need to generate the Embed for the Viewer to load. In Vectary, open the Embed tab located in the right panel and choose appropriate quality settings for baking and textures. Once generated, you are ready to place the Viewer on your website.

## Load the viewer

To load the Viewer into your website, you can either use an iframe or a web component (recommended). 

To use our `<vctr-viewer>` web component, you need to include three Javascript files:
- `webcomponents-loader.js` - Library of polyfills to make sure Web components work in legacy browsers
- `vctr-viewer.js` - Vectary Viewer application
- `api.js` - Vectary Viewer API - if you intend to use [API methods](methods.md)

Viewer in web component with API enabled:

```html
<head>
    <script type="text/javascript" src="https://unpkg.com/@webcomponents/webcomponentsjs@2.2.7/webcomponents-loader.js"></script>
    <script type="module" src="https://www.vectary.com/viewer/v1/scripts/vctr-viewer.js"></script>
    <script type="module">
        import { VctrApi } from "https://www.vectary.com/viewer-api/v1/api.js";
        //Your Viewer API magic here
    </script>
</head>
<body>
    <vctr-viewer 
        id="d6c1f27d-6a27-4c7e-bd7d-bd19d7faa56c" 
        model="d6c1f27d-6a27-4c7e-bd7d-bd19d7faa56c" 
        enableApi=1">
    </vctr-viewer>
</body>
```

If you prefer, you can load the Viewer via `<iframe>`:

```html
<head> 
    <script type="module">
        import { VctrApi } from "https://www.vectary.com/viewer-api/v1/api.js";
        //Your Viewer API magic here
    </script>
</head>
<body>
    <iframe 
        id="d6c1f27d-6a27-4c7e-bd7d-bd19d7faa56c" 
        src="https://www.vectary.com/viewer/v1/?model=d6c1f27d-6a27-4c7e-bd7d-bd19d7faa56c&enableApi=1" 
        frameborder="0" 
        width="100%" 
        height="480">
    </iframe>
</body>
```

?> If you do not plan to use any API methods in your project (e.g. for object visibility manipulation, camera switching etc.) you do not need to include the `api.js` script in your head or enable the API via `enableApi=1` parameter. To only use the [Viewer parameters](parameters.md) (e.g. turntable, autoplay etc.) API is not necessary.

## Simple initialization of the Viewer API

Once the Viewer is loaded, you're all set to use the [API](methods.md) to further control Viewer's behavior or to add your own logic.

!> To be able to use the API, the `api.js` script needs to be loaded and enableAPI parameter needs to be enabled `enableAPI=1`. See the [complete list of parameters](parameters.md) for additional controls.

See the example script below. Once the API is successfully initialized, it will log the list of all objects available in the Viewer.

```javascript
import { VctrApi } from "https://www.vectary.com/viewer-api/v1/api.js";

const viewerApi = new VctrApi("d6c1f27d-6a27-4c7e-bd7d-bd19d7faa56c");

async function run() {    
    await viewerApi.init();
    console.log(await viewerApi.getObjects())
}

run();
```

> See the [live demo](https://codepen.io/vectary/pen/BaBgaQe?editors=1011)

## Initialize the Viewer API with error handling

Example below shows how to initialize the Viewer API with the proper error handling.

```javascript
import { VctrApi } from "https://www.vectary.com/viewer-api/v1/api.js";
let viewerApi;

async function run() {    

    function errHandler(err) {
        console.log("API error", err);
    }

    async function onReady() {
        console.log("API ready");
        try {
            console.log(await viewerApi.getObjects());          
        } catch (e) {
            errHandler(e);
        }
    }

    viewerApi = new VctrApi("d6c1f27d-6a27-4c7e-bd7d-bd19d7faa56c", errHandler);

    try {
        await viewerApi.init();        
        onReady();
    } catch (e) {
        errHandler(e);
    }
}

run();
```

From here, it's up to your imagination. Go ahead and experiment with Viewer API [parameters](parameters.md) and [methods](methods.md).