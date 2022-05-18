# Creating App Actions

This article will show you how to create app actions in the TDK. Click on 'Create App Action' and fill in the fields when it asks for a name and description.

![screenshot.30](https://docs.toca.io/hs-fs/hubfs/book%20of%20toca%20images/IPL/IPL%20TDK/screenshot.30.jpg?width=602&name=screenshot.30.jpg) 

 
This will create a template of an empty app action.

![screenshot 1](https://docs.toca.io/hs-fs/hubfs/book%20of%20toca%20images/IPL/IPL%20TDK/screenshot%201.png?width=602&name=screenshot%201.png) 
 
App actions are typescript transpiled into a JS web worker. Web workers are separate files that the DOM thread of a website can spawn. They are run in a separate thread, meaning that any computation done in them won't block the UI. The DOM thread and workers communicate through messages.
 
You can see in the template self.onmessage is set to call the main run function; this means that anytime this worker receives a message it will call that function. Therefore, when creating an app action you only need to worry about updating the run function.
 
In order for the app action to communicate to the main thread that it is finished, the app action needs to send a message back. To do this the template provides two useful functions: createReply and createError; these will post a message back to the main thread and use the data passed in as the outputs of the app action.
 
To learn more about web workers, click [**here**](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers)


Just like app components, if you want to use a library then create a package.json file in the root folder with your dependencies.

```json

{
    "dependencies": {
        "lodash": "^4"
    }
}
```











You will then be able to import them into the app action.
 
