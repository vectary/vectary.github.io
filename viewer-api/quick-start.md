## Prepare your Embed

If you haven't done so already, head to [Vectary](https://www.vectary.com) and start a new project. Create your models either by modelling from scratch or by importing from other tools or 3D libraries.

Once you're happy with your scene, you will need to generate the Embed for the Viewer to load. In Vectary, open the Embed tab located in the right panel and choose the appropriate quality settings for baking and textures. Once generated, you are ready to place the Viewer on your website.

## Viewer load

To load the Viewer into your website, you can either use an iframe or a web component.

?> We recommend using the [web component](https://developer.mozilla.org/en-US/docs/Web/Web_Components) whenever possible, since this allows the viewer to reside within the same [Window](https://developer.mozilla.org/en-US/docs/Web/API/Window), whereas an [iframe](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) has its own. It is also easier to add, delete or modify the parameters used.

To use our `<vctr-viewer>` web component, you need to include one to three Javascript files:
- `vctr-viewer.js` - Vectary Viewer application
- (optional) `webcomponents-loader.js` - Library of polyfills to make sure Web components work in legacy browsers
- (optional) `api.js` - Vectary Viewer API - if you intend to use [API methods](methods.md)

Viewer in web component:

```html
<head>
    <script type="text/javascript" src="https://unpkg.com/@webcomponents/webcomponentsjs@2.2.7/webcomponents-loader.js"></script>
    <script type="module" src="https://www.vectary.com/viewer/v1/scripts/vctr-viewer.js"></script>
    <script type="module">
        import { VctrApi } from "https://www.vectary.com/viewer-api/v1/api.js";
        // Your Viewer API magic here
    </script>
</head>
<body>
    <vctr-viewer
        id="model_X"
        model="d6c1f27d-6a27-4c7e-bd7d-bd19d7faa56c">
    </vctr-viewer>
</body>
```

If you prefer, you can load the Viewer via `<iframe>`:

```html
<head>
    <script type="module">
        import { VctrApi } from "https://www.vectary.com/viewer-api/v1/api.js";
        // Your Viewer API magic here
    </script>
</head>
<body>
    <iframe
        id="model_X"
        src="https://www.vectary.com/viewer/v1/?model=d6c1f27d-6a27-4c7e-bd7d-bd19d7faa56c"
        frameborder="0"
        width="100%"
        height="480">
    </iframe>
</body>
```

?> If you do not plan to use any API methods in your project (e.g. for object visibility manipulation, camera switching etc.) you do not need to include the `api.js` script in your head. To only use the [Viewer parameters](parameters.md) (e.g. turntable, autoplay etc.) the API is not necessary.

## API Initialization

Once the Viewer is loaded, you're all set to use the [API](methods.md) to further control Viewer's behavior or to add your own logic.

!> To be able to use the API, the `api.js` script needs to be loaded. We recommend importing it as an ES Module.

See the example script below. Once the API is successfully initialized, it will log the list of all objects available in the Viewer.

```javascript
import { VctrApi } from "https://www.vectary.com/viewer-api/v1/api.js";

const viewerApi = new VctrApi("model_X"); // DOM Id

async function run() {
    await viewerApi.init();
    console.log(await viewerApi.getObjects())
}

run();
```

> See the [live demo](https://codepen.io/vectary/pen/BaBgaQe?editors=1011)

## Error handling

The API constructor allows to pass a function which will be used to pass along all error messages. If no function is specified you can handle the errors on a `try/catch` block or using the `then/catch` promises formula.

The example below shows a couple of ways how to set proper error handling with the same function, but you can create more error handling functions to be used in different parts of your particular application.

```javascript
import { VctrApi } from "https://www.vectary.com/viewer-api/v1/api.js";

// We have two models in the page
const viewerApi_X = new VctrApi("model_X", errHandler);
const viewerApi_Y = new VctrApi("model_Y");

async function run() {

    async function onReady() {
        console.log("API ready");

        console.log(await viewerApi_X.getObjects());
        await viewerApi_Y.getObjects()
            .then((objects) => console.log(objects))
            .catch(e => errHandler(e));
    }

    await viewerApi_X.init();
    try {
        await viewerApi_Y.init();
    } catch (e) {
        errHandler(e);
    }
    onReady();
}

function errHandler(err) {
    console.warn("API error:", err);
}

run();
```

From here, it's up to your imagination. Go ahead and experiment with [parameters](parameters.md) and [methods](methods.md)!
