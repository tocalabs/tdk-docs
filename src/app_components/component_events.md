# Component Events

A component can trigger an event which will then trigger an app action. For example, a component could have an onClick event which the user could use to call an app action to redirect to a different page.
To add events, go to the 'Events' tab on a component in the TDK. Here you can add/edit/delete the events of a component. To add the default events you can click the wand icon.

![screenshot4](https://docs.toca.io/hs-fs/hubfs/book%20of%20toca%20images/IPL/IPL%20TDK/screenshot4.png?width=688&name=screenshot4.png) 

 
The information provided here will be shown in the event viewer, allowing the user to know what the event does and any outputs that come with the event.
>  Note: It is important that the Key matches the key used with the fireEvent call.

![screenshot5](https://docs.toca.io/hs-fs/hubfs/book%20of%20toca%20images/IPL/IPL%20TDK/screenshot5.png?width=688&name=screenshot5.png) 

 
The component then needs to implement the event. It does this by using the useAppEvents hook from the @tocabot/sdk. To fire the onInit event shown above you could use the code below.

```typescript
import { useAppEvents } from '@tocabot/sdk';

...
// Usually makes sense for the onInit event to be fired in a useEffect
fireEvent('onInit', id, eventListener);

```

The fireEvent function parameters are:
- Event Name 
    - The key that you entered when adding the event
- ID
    - The ID of the component
- Additional Parameters
    - Any payload of the event can then be given in the order that was set
    - There is no limit to the number of additional parameters

 
