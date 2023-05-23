# Tocabot SDK Library

The tocabot SDK is a library that holds React components, helper functions and React hooks.  

## Components

### DynamicDataChipInput

`DynamicDataChipInput` is a component that allows the ability to accept both normal text input (Number/Boolean/String) but also provides the UI to use a Datachip for the value.

#### Props

|prop|desc|type|default value|
|-|-|-|-|
|`label`| The label to show on the input field| `string` | - |
|`value`| The value of the input | `string \| boolean \| number \| DashDataChipEntity` | - |
|`onChange`| The onChange function | `(value: string \| boolean \| number \| DashDataChipEntity \| undefined) => void`| - |
|`kind`| The kind of parameter | `Number \| Boolean \| String \| Any \| Array \| Table`| - |


#### Example
```ts
<DynamicDataChipInput
    label="Name"
    kind="String"
    value={name}
    onChange={value => onChange({ name: value })}
/>
```

This is accessed via the `useDashDataChipValue` hook:

```ts
    const [variable] = useDashDataChipValue<string>(options.variable, ['string']);	 
```

### InlineAppDataChipInput
`InlineAppDataChipInput` is a component that allows for Datachips to be added inline with other text values. This can be useful for composite values. For example if you wanted to add a datachip of page context to a static string.

#### Props

|prop|desc|type|default value|
|-|-|-|-|
|`label`|The label to show on the input field|`string` | - |
|`value`|The value of the input|`InlineAppChipPart[] \| string` | - |
|`onChange`|The onChange function|`(value: InlineAppChipPart[]) => void` | - |

#### Example

```ts
<InlineAppDataChipInput
    label="Label"
    value={label}
    onChange={(value) => onChange({ label: value })}
/>
```
> An example of this can be found in the options of `Text Field`


### SlotContainer

The `SlotContainer` is a component that can be used to manage the creation of slots in app designer. A `slot` is a space where an app designer can place other components inside of it. This can then be used for displaying a custom app designed layout without hard coding it in the component.

#### Props

|prop|desc|type|default value|
|-|-|-|-|
|`componentId`|The id of the component it is being used in|`string` | - |
|`slot`|The name of the slot. This can then be used for retriving the slot in the non builder view|`string` | - |
|`selectable`|If the slot can be selected of not|`boolean` | `false` |
|`selectedId`|The id of the selected component| `string` | - |
|`filter`| A function to filter slots | `(entity: { id: string; kind: string }) => boolean`| - |
|component| The component to use to wrap the slot | `React.Component \| string` | `div` |

#### Example

```tsx
const slotName = "test";
<SlotContainer
    componentId={id}
    slot={slotName}
    selectable
    selectedId={selectedId}
>
    {slots[slotName]}
</SlotContainer>
```

> `slots` is a prop that can be used from the props passed into the app component. A good example of this in use is the `Responsive Grid`


## Hooks

### useDashDataChipValue

`useDashDataChipValue` is a hook that allows you to retrive the value of a datachip. This is useful for options that you have are defined as datachips.

The hook returns an array of values `[value, loading, error]` with the types `[ParameterEntity<T> | undefined, boolean, string | undefined]`. 

#### Parameters

|parameter|desc|type|default value|
|-|-|-|-|
|`chip`|The chip that the value is to be retrieved from | `T \| DashDataChipEntity \| undefined` | - |
|`validTypes`| Optional array of types that can be accepted | `string[]` | - | 

#### Example

```ts
const [param, loading, error] = useDashDataChipValue(chip, ['string']);
```

### useDashDataChipValueQuery

`useDashDataChipValueQuery` is a hook that allows for a query to be provided in addition to any query the is on the chip. The query and limits prvoided to this hook can be flagged to override any query on the chip. By default it will not be overriden.

#### Paramters

```ts
export interface Overide<T> {
	value?: T;
	overide?: boolean;
}
```

|parameter|desc|type|default value|
|-|-|-|-|
|`chip`|The chip that the value is to be retrieved from | `T \| DashDataChipEntity \| undefined` | - |
|`validTypes`| Optional array of types that can be accepted | `string[]` | - | 
|`options`| The options that can be provided to override the query, limit, offset etc. | `{ query?: Overide<QueryEntity>; limit?: Overide<number>; offset?: Overide<number>;orderColumns?: Overide<string>; orderBy?: Overide<string>;}`| - | 

#### Example

```ts
const [dataChipValue, loading, error] = useDashDataChipValueQuery<DataTableEntity>(dataSource, [
		'table',
	], {
		...(limit ? {limit: { value: limit, override: true}}: {})
	});
```

### useDashDataChipValueInfo

`useDashDataChipValueInfo` is a hook to get the information about a chip. This is mainly used for getting the information about datachip tables. Although this is likely to be expanded in the fututre. 

#### Parameters
|parameter|desc|type|default value|
|-|-|-|-|
|`chip`|The chip that the value is to be retrieved from | `T \| DashDataChipEntity \| undefined` | - |

#### Example
```ts
const info = useDashDataChipValueInfo(dataSource);
```

### useInlineChipValue 

`useInlineChipValue` is a hook that can be used to get the value when using the `InlineAppDataChipInput`. 

#### Parameters

|parameter|desc|type|default value|
|-|-|-|-|
|`part`|The Inline chip value returned from the component | `InlineAppChipPart[] \| string \| null \| undefined` | - |
|`coerceMethod`|A method that can be provided to coerce the returned value into a certain format| `(param: ParameterEntity<any> | undefined) => ParameterEntity<string> \| undefined` | - |

#### Example

```ts
const coerceMethod = (param) => {
	if (param && param.type.toLowerCase() === 'file') {
		return {
			key: param.key,
			type: 'String',
			value: param.value.fileName ? param.value.fileName : param.value,
		}
	}
	return param;
}

const parsedButtonText = useInlineChipValue(buttonText, coerceMethod);
```


### useAppEvents

`useAppEvents` is a hook to provide IPL functions/values to components. The functions can then be used inside of the component.

#### Values/Functions

##### fireEvent
`fireEvent` allows an event to be fired for that component

###### Usage
```ts
const { fireEvent } = useAppEvents();
fireEvent('onEvent',id, param1, param2);
```

> 'onEvent' - The event that has been defined in the events tab

> id - The id of the component

> param1, param2 - Paramters that have been defined in the payload of the events tab. These are optional and more can be added by adding them to the end of the parameters

##### workerLoaded

`workerLoaded` is a boolean value that references if the main web worker is loaded. This is responsible for executing the app actions. Therefore, it is useful for when firing an event on load of a component, to ensure it is only fired once the event had been loaded. 

###### Usage
```ts
const { fireEvent, workerLoaded } = useAppEvents();

useEffect(() => {
    if (workerLoaded) {
        fireEvent('onInit', id);
    }
}, [workerLoaded]);
```