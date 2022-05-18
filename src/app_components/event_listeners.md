# Event Listeners

Event listeners are a way for components to listen for certain events so that they can trigger a function. This can be useful for updating a value through in page logic. The component is responsible for defining and registering eventListeners. Event listener names should be defined in the options of a component so that they can be customised by the user, but should always have a default value for that instance of the component.
To define an event listener go to the 'Event Listener' tab on the component in the TDK. Here you can add/edit/delete the event listeners for a component. You need to define the 'Options Name' and the 'Description'.

- Option Name
    - The property value that is used in the options of the component for the user to override the eventListener name.
- Description
    - Describe what the eventListener does. E.g 'Update the text value of the text field'


![image.png](https://tocabot.visualstudio.com/0dd64ef6-a3e6-45d6-ad6f-acef49be7fc3/_apis/git/repositories/7919de95-7b58-4952-a06c-62c5d6d10d8a/Items?path=/.attachments/image-9e3ca7d5-9c4e-4576-b582-93ce5ff093e1.png&download=false&resolveLfs=true&%24format=octetStream&api-version=5.0-preview.1&sanitize=true&versionDescriptor.version=wikiMaster) 

 
For the above eventListener definition you would need to add this to the options

```typescript
options: { testEventListener = `${id}_test` },
```

It is important to give it a default value that is related to the INSTANCE of the component. If the eventListener matches the name of another, both event listeners will be fired.

### Registering an eventListener

To call an event listener you first need to register the eventListener on the component use the addListener function from the useAppEvent hook. To ensure that it is registered correctly it is important to first make sure that the worker is loaded. You can do this by using the workerLoaded variable that is provided by the same hook.

```typescript
const { addListener, workerLoaded } = useAppEvents();

useEffect(() => {
    // When worker loaded add listener for updating text field
    if(workerLoaded){
        addListener({
            id, 
            listenerName: textFieldUpdateListener,
            run: msg =>; {
                form?.onChange(msg.data);
            }
        });
    }
}, [workerLoaded]);

```

The addListener function takes

- id
    - The id of the component that it is registered too  
- listenerName
    - The name of the listener for that instance
- run
    - A function to be performed when loading



### Calling an event Listener


To call an event listener you can use the 'Trigger Event Listener' app action. Simply drag it on to the event viewer and link it up to an event or other app action. You will then need to fill in the event listener and the data to send. The event listener should be for the instance of the component you want to update. You can do this manually by typing in the value yourself OR you can use the datachip which will dynamically use the event listener for the component you select (even if you update the event listener in the options of that component)

![image.png](https://tocabot.visualstudio.com/0dd64ef6-a3e6-45d6-ad6f-acef49be7fc3/_apis/git/repositories/7919de95-7b58-4952-a06c-62c5d6d10d8a/Items?path=/.attachments/image-31dea35f-540a-47f6-b138-32a8857fdfd6.png&download=false&resolveLfs=true&%24format=octetStream&api-version=5.0-preview.1&sanitize=true&versionDescriptor.version=wikiMaster) 

 
First, select the component that you want to trigger. (You can rename components in the properties panel of the component).

![image.png](https://tocabot.visualstudio.com/0dd64ef6-a3e6-45d6-ad6f-acef49be7fc3/_apis/git/repositories/7919de95-7b58-4952-a06c-62c5d6d10d8a/Items?path=/.attachments/image-ccc14255-8a47-40d2-9150-afd6d7419960.png&download=false&resolveLfs=true&%24format=octetStream&api-version=5.0-preview.1&sanitize=true&versionDescriptor.version=wikiMaster) 

 
Then select the eventListener you want to call and press insert. This will insert it as a data chip

![image.png](https://tocabot.visualstudio.com/0dd64ef6-a3e6-45d6-ad6f-acef49be7fc3/_apis/git/repositories/7919de95-7b58-4952-a06c-62c5d6d10d8a/Items?path=/.attachments/image-573dac2c-4f5a-4b21-b6f2-1aa6e6f14988.png&download=false&resolveLfs=true&%24format=octetStream&api-version=5.0-preview.1&sanitize=true&versionDescriptor.version=wikiMaster) 

 
The data value should be the value that you want to pass to the component. This can be ANY type (default will be string) and you can use an output from another app action or event if you want to.
 
