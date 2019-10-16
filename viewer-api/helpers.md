
# Helpers

To make your life easier, we have prepared API Helpers that bundle together multiple API methods, so you can get results faster. We will continuously add more Helpers based on your feedback.

## Methods

### animate()
Helper function for animating the api method calls and executing them within the time frame.
- Input: Duration of animation in ms (number). Time function callback or string for modifying the animation, usually used for easing. Possible easing arguments are: "linear", "easeInQuad", "easeOutQuad", "easeInOutQuad", "easeInCubic", "easeOutCubic", "easeInOutCubic", "easeInQuart", "easeOutQuart", "easeInOutQuart" Draw function or api method call. On finish function callback (executes when the animation is done).
- Returns: Nothing

```javascript
const currentPosition = await viewerApi.getPosition("Rocks");           
function animation() {
  VctrApi.Utils.animate(
    3000,
    "easeOutQuad",
    (timeFraction) => {
      const position = VctrApi.Utils.lerp(currentPosition, [0, 0, 2], timeFraction);
      viewerApi.setPositionAbsolute("Rocks", position);
    }
  );
}
animation();
```

> See the [live demo](https://codepen.io/vectary/pen/pozpjmB?editors=1011)

### lerp()
Helper function for linear interpolation of two vectors (usually used with absolute transformations).
- Input: First vector ([number, number, number]). Second Vector ([number, number, number]). Alpha value (number).
- Returns: [number, number, number]

