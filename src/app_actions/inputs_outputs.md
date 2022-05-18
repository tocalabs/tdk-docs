# Inputs & Outputs

### Inputs

App actions can have inputs to them for the app action to use. To declare inputs, first you must go to the inputs tab and configure the inputs.

![screenshot2](https://docs.toca.io/hs-fs/hubfs/book%20of%20toca%20images/IPL/IPL%20TDK/screenshot2.png?width=688&name=screenshot2.png) 

 
You can provide helper text and options if the selection should be from a set list. Make sure that you set the type so it's clear to the user what you are expecting the value to be. This will be used to determine what is shown on the input's UI in the event viewer.
Next add the input to the RunProps interface and the value destructured object in the parameters of the run function.
>  Make sure that the variable name is the key of that you entered in the inputs panel

```typescript
interface RunProps {
    myInput: string;
}

function run({ myInput }: RunProps) {
    // Ensure a post is made to ensure that the worker terminates and triggeres the next action
    createReply({});
}
```

You are now able to use the input inside of the app action.

### Outputs


App actions also have outputs which allow for app actions to be chained using the output of one as the input of the other.
To set an output, first go to the outputs panel and set the label, key and type. Like with the inputs, make sure to set the correct type to help the user when using the output in the event viewer.

![screenshot3](https://docs.toca.io/hs-fs/hubfs/book%20of%20toca%20images/IPL/IPL%20TDK/screenshot3.png?width=688&name=screenshot3.png) 
 
You can then use the output in a createReply call. Again, make sure to use the key of the output that you typed into the outputs panel.

```typescript
createReply({ myOutput: myInput});
```

 
