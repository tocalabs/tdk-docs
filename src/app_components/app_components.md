# App Components

In the TDK you can build app components that can be used in an app. Components are built in React and can import any package required (assuming the package is declared in the package.json).

## App components structure 

The structure of the app component is important as it is currently used to detect what file to use for the component and what file to use for the options that are shown in the app designer. The folder structure is:

```
Source/
---> package.json (if importing more packages)
---> src/
-------> index.tsx (entry file for the component)
-------> options.tsx (entry file for the component options)
```

> __Note__: these are just the base files. You can add as many files/folders in the TDK as you want.

The `index.tsx` is the entry file for the app component. This is what is used for both desgin/preview and published versions of the app component. (Later we will go into how we check if it's in deign mode or not)

The `options.tsx` is the entry file for the options of the app component. This allows you to customise the options that are shown for that app component. This allows for a richer customosable experience for your options instead of the usual JSON configuration for options in other products. 

## App Component props

The app component props are:
```ts
	/**
	 * ID of the app component instance
	 */
	id: string;

	/**
	 * Index of the component in it's parent
	 */
	index: number;

	/**
	 * Component instance options
	 */
	options: Options;

	/**
	 * Component styles to apply to the root element
	 */
	style: CSSProperties;

	/**
	 * Slots containing the component's children
	 */
	slots: Record<string, ReactNode>;

	/**
	 * Options for the above slots
	 */
	slotOptions: Record<string, SlotOptions>;

	/**
	 * Classes to apply to various elements in the component.
	 */
	classes: { root: string } & Record<string, string>;

	/**
	 * True if the component is being rendered inside the app builder.
	 */
	inBuilder?: boolean;

	/**
	 * Id of the selected component or slot
	 */
	selectedId: string | null;
```

The `inBuilder` prop can be used to provide a different user experience for when in the app designer compared to app preview OR a published app. 

For the options the props are:

```ts
interface Props {
	id: string;
	options: Partial<Options>;
}
```

The props for the `options.tsx` simply provide the id of the component (unique to the instance of an app component) and the options for that instance of the app component. 

> __Note__: You need to define the `Options` interface in the `options.tsx` to ensure that the options are known with their releavant types.

### Options hook
As app component options are fully customsiable we need a standard way to update the option values.

To ensure a standard approach you can use the `usePropertiesChange` hook that is imported from `@tocabot/sdk`. 

> __Note__: This is created for you in the app component template that is generated when creating the component. 

```ts
const onChange = usePropertiesChange(id);
```

This means to change an options value in the options panel you can do the following.

```ts
onChange({
	option1: 'hello',
	option2: 'world',
})
```

## Using npm packages in app components

You can extend the dependencies that app components can use. To do this all you need to do is add a `package.json` at the same level as the `src` folder. There dependencies that will be already imported are:
```json
{
	"react": "16.13.1",
	"react-dom": "16.13.1",
	"@material-ui/core": "4.9.10",
	"@material-ui/lab": "4.0.0-alpha.45",
	"@tailwindcss/typography": "0.2.0",
	"tailwindcss": "1.7.6",
}
```

> __Note__: These will be updated with the core version of the packages

To add more dependencies simply add a `dependencies` property adding additional dependcies you want to use. These will be merged with those that are added by default.

```json
{
    "dependencies": {
        "@u-wave/react-vimeo" : "0.9.5"
    }
}
```

## Using IPL in app components
In page Logic (IPL) is a way for users to trigger logic of partcualr app component events. These events are defined by each app component and can be customised to pass through as much or as little data as required. 

For example, if we are creating a button, we will want the `onClick` event to trigger an action. To ensure that this action isn't hard coded and can be extended by the app designer at a later stage we can instead fire an event through IPL, which will allow the app designer to then hook up their own logic at app design time.

To add an onClick event to our button component, we are going to:

1.  Go to the `Events` tab at the bottom of the TDK screen.
2.  Press the add button
3. 	Add the following values

|Field|Description|Value|
|-|-|-|
|icon|The icon to be shown in the app designer drag and drop interface|(A relevant icon for the action)|
|label|A descriptive label of the event|Click|
|key| The key of the event. This needs to match the string entered in the `fireEvent` hook | onClick|
|Description|A description of the event|Fires when an element has been clicked|
|Payload|If any values are being passed from the event then add them to the payload to app designer know what values they can use from this event |n/a|

4. Add `fireEvent` where the event should be fired.

```ts
// other imports
import { useAppEvents } from '@toabot/sdk';

// inside of app component function
const { fireEvent } = useAppEvents();
// Fire the IPL event on function being called. useCallback to ensure the id is up to date.
const onClick = useCallback(() => {
	fireEvent(id, 'onClick');
}, [id]);
```

The `fireEvent` hook takes 2+ parameters. 
1. id - The id of the app component. This can be passed from the props of the app component
2. key - The key of the event to fire. This MUST be the same as the one declared in the events tab.

Any other paramters passed to the function will be treated as the payload that has been defined in the events tab. So if you had additional data to pass from the event, you can just add them to the fucntion in the order provided in the payload events tab. 
