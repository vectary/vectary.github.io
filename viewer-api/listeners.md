# Event Listeners

Event Listeners API follows general event listener pattern that you might know from other areas. You can subscribe and unsubscribe to receive updates through callback methods. Please note you are limited to one callback method per one event type.

## General usage

This section describes adding and removing event listeners in general.

### addEventListener()
Adds event listener to specified event. Adding another listener to an event you are already subscribed to will replace the previous listener.
- Input: 
- - Event Type ([ApiEvent](/enumerations?id=eventtype)) - This parameter can be passed as a string value of the [ApiEvent](/enumerations?id=eventtype) enumeration item. Other options is to access this enumeration directly as a static member of the **VctrApi** object, for example `VctrApi.ApiEvents.ORBIT_CONTROLS_STATE_CHANGE`.
- - callback - Callback function with one parameter that will contain **event data**.
- Returns: boolean

### removeEventListener()
Removes event listener from specified event. Since there is one listener per object, this function only needs event type passed in.
- Input: Event Type ([ApiEvent](/enumerations?id=eventtype)) - This parameter can be passed as a string value of the [ApiEvent](/enumerations?id=eventtype) enumeration item. Other options is to access this enumeration directly as a static member of the **VctrApi** object, for example `VctrApi.ApiEvents.ORBIT_CONTROLS_STATE_CHANGE`.
- Returns: boolean

## Event Types

Following are events that you can subscribe to.

### Orbit controls state change

Use this event to keep track of these interaction states of your scene:

- Rotation
- Panning
- Dollying
- None

Every time your scenes state transitions from one state to another your callback will be called. Fox example for simple rotation this event will fire twice, first time for `none` to `rotation` transition and second time for `rotation` to `none` transition.

**Event Data:**
- oldState: "NONE" | "ROTATE" | "DOLLY" | "PAN" | "TOUCH_ROTATE" |  "TOUCH_DOLLY_PAN"
- newState: "NONE" | "ROTATE" | "DOLLY" | "PAN" | "TOUCH_ROTATE" |  "TOUCH_DOLLY_PAN"

**Event Type:**
- Enumeration value: `VctrApi.ApiEvents.ORBIT_CONTROLS_STATE_CHANGE`
- String value: "ORBIT_CONTROLS_STATE_CHANGE"

```javascript
vctrApi.addEventListener(VctrApi.ApiEvents.ORBIT_CONTROLS_STATE_CHANGE, (eventData) => {
    console.log(eventData.oldState, "->", eventData.newState);
});
```


