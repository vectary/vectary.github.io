
# Helpers

To use helpers include them in your code like this:
```html
  <script type="module">
    import { animate } from "https://www.vectary.com/embed/viewer/v1/scripts/api/apiUtils.js";
    //Your Viewer API magic here
  </script>
```


## Methods

### animate(duration: number, timing: function, draw: function, onFinish: function)
Helper function for animating the api method calls and executing them within the time frame.
- Input: Duration of animation in ms. Time function for modifying the animation, usually used for easing. Draw function or api method call. On finish function callback (executes when the animation is done).
- Returns: Nothing

```javascript
animate(
    1000,
    timeFraction => { 
        return Math.pow(timeFraction, 2);
    },
    () => {
        vctrApi.setRotation("Cube", [0, 0, 90]);
    }
);
```