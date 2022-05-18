
# TDK Action Helpers
 
Action helpers allow you to extract common functionality shared between actions to a separate class. This way you can use this functionality without having to repeat yourself. Helpers are effectively libraries of useful classes and methods which you can leverage and use in any action.

#### Create/Edit an Action Helper

Let's have a look at an existing helper to get an overview of how to add or edit a helper.
 
Click on the OPEN EXISTING button on the TDK.

![Image](https://docs.google.com/drawings/u/0/d/spzsDf0xQrH7WfP4N1wKd-g/image?w=584&h=370&rev=8&ac=1&parent=1021Hys0a2A5pml4_OnXLucoUj01SY38hCWhwtsvqraM) 

Click on the Helpers option to show all the existing helpers.

![Image](https://docs.google.com/drawings/u/0/d/sx05epVhNSwXZi7li_JzcEw/image?w=602&h=324&rev=7&ac=1&parent=1021Hys0a2A5pml4_OnXLucoUj01SY38hCWhwtsvqraM) 

Open any helper that is available on your platform and you'll see a similar interface to the one in the screenshot below.

![Image](https://lh4.googleusercontent.com/WzOXgGkC7XJ9qB3y-xQaXbhYSYqzucPs4EsiWS-26r00FNbzYrpPQ9EsN8RuF58ltHIUdECemvEaF4lWGmKUcfeeZ1ZLUBYFFxTYmmTO_dOqyospBPfAjQIY-9xarnUuTsO_-yWW) 

 
Unlike the Action IDE, the Helper IDE doesn't have any inputs or Bot components as a helper is purely made up of code. Currently helpers only support a single file so if your helper requires multiple classes you'll have to write them all in a single file.
Like actions, the Helpers are written in C# and use the .NET 6 framework.

#### Add a Helper to an Action

To add a helper to an action you can open an action and find the Helpers tab.

![Image](https://docs.google.com/drawings/u/0/d/s-TbrWpdY13078NmAeTd-mQ/image?w=602&h=264&rev=7&ac=1&parent=1021Hys0a2A5pml4_OnXLucoUj01SY38hCWhwtsvqraM) 

Just tick the helper you want to use in the action and that's all you need to do.

![Image](https://lh6.googleusercontent.com/7Dcn37or7GAeDtY55QVUhN0fe0ihZLPJ-4qrRzr0gDzP6STxxelnpdsa61LR1gk6DSP6Vy-uw78CPGEyOEkUyZthw9-pz757rnFDmRU0WCJBhuPfziP5VDqYIEbqJTSK6TXvK7PO) 


#### Testing a Helper

As helpers are simply a library of functions they are a bit more difficult to test than actions so the approach to testing is different. Whereas with Actions you test them by using them in a draft state to check everything is as expected, you write unit tests for helpers.
Open a helper and locate the Unit Tests tab.

![Image](https://lh4.googleusercontent.com/VSV4jJ46mkCrXyal3YfuP0xb6oIVQq-GyBvY2jlb6_jnXmJ9SrIoEEPhJaYbS-PcuMF5YZTOw_NyJs3F9pUsVFrWdsfPdNKMC82wBBS8tjV5XkpPp8zlXnzblad_NbkkvcLFdBLI) 

You'll see that a test template is set up for every helper and existing helpers may already have unit tests written for them.
You can run a test by... (TBC)

#### Publish a Helper

Like actions and app components you can publish them to the Hub so that other Toca platforms can use the helper you have written.
When you are happy with your helper and it has been tested thoroughly, find the *Push Helper* button which is in the top right corner of the Action Helper IDE.

![Image](https://docs.google.com/drawings/u/0/d/saUpINAzVKY2miLDYESf3rA/image?w=259&h=164&rev=7&ac=1&parent=1021Hys0a2A5pml4_OnXLucoUj01SY38hCWhwtsvqraM) 

 
