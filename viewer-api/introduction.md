## Fellow developers &#128406;

> Welcome to the Vectary Viewer API. A powerful development tool that lets you create amazing interactive 3D applications for the web.

## Vectary Viewer

?> Vectary is the easiest online 3D design & 3D modeling software on the web. For more information visit [Vectary homepage](https://www.vectary.com). To learn the basics of 3D modelling in Vectary, see the [Vectary Documentation](https://www.vectary.com/docs/).

As the only service out there, **Vectary** along with **Vectary Viewer** will cover your needs both in terms of creation and online presentation of your 3D work.

In it's simplest form, the Viewer generated in Vectary editor, can be used as an iframe.

```html
<iframe 
    id="d6c1f27d-6a27-4c7e-bd7d-bd19d7faa56c" 
    src="https://www.vectary.com/viewer/v1/?model=d6c1f27d-6a27-4c7e-bd7d-bd19d7faa56c&turntable=-2" 
    frameborder="0" 
    width="100%" 
    height="480">
</iframe>
```
The line of HTML above will result in interactive 3D model loaded directly into your website. Try rotating, zooming or panning the scene. When viewed on supported mobile devices both on iOS (Safari) and Android (Chrome), AR icon will show up for users to see the model in the real-world.

<iframe id="d6c1f27d-6a27-4c7e-bd7d-bd19d7faa56c" src="https://www.vectary.com/viewer/v1/?model=d6c1f27d-6a27-4c7e-bd7d-bd19d7faa56c&turntable=-2" frameborder="0" width="100%" height="480"></iframe>

## Vectary Viewer API

The Viewer API lets you build web projects on top of Vectary Viewer. 

+ [Parameters](/parameters)
+ [Methods](/methods)
+ [Types](/types)
+ [Helpers](/helpers)


?> Feel free to reach out to our support team and other developers on [Spectrum](https://spectrum.chat/vectary). Let us know, what you're building, we are happy to help.

## Examples

To give you some examples and to inspire you, we’ve put together a list of interesting projects built with Vectary Viewer API.

- Viewer API showcase - [Demos](https://www.vectary.com/viewer/demo/)
- Texture replacing and screenshot taking (as used in Figma plugin) - [Demo](https://plugin-demo.vectary.now.sh), [Source](https://github.com/vectary/plugin-demo)
- Interactive festival map - [Demo](https://grape-festival-map.vectary.now.sh/?lang=en), [Source](https://github.com/vectary/grape-festival-map)
- Product configurator: Helmet - [Demo](https://pocsports-demo.vectary.now.sh/), [Source](https://github.com/vectary/pocsports-demo)
- Product configurator: Chair - [Demo](https://stokke-demo.vectary.now.sh/), [Source](https://github.com/vectary/pocsports-demo)
- Video texture - [Demo](https://lyft-demo.vectary.now.sh/), [Source](https://github.com/vectary/lyft-demo)

## Version

To set the version change the “v1" in iframe or script src properties.

- Viewer:
 - v1: Version 1.0 - Stable
- API:
 - v1: Version 1.0 - Stable

## Changelog

- Dec 3, 2019
 - API v1: 1.0 Stable
 - New arIcon and showPlaceholder parameters
 - New takeScreenshot method
 - See all [changes](https://github.com/vectary/vectary.github.io/commits/master)

- Sept 6, 2019
 - API v1: 1.0 Beta 
 - This version is stable, no breaking changes will be implemented in v1. Some API methods still need improving.

- July 1, 2019
 - API v1: 1.0 RC 
 - Releasing the first version of the Viewer API. Things are still under development and your projects might break in the future.
