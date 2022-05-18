
# Introduction to TDK

Included with every Toca platform is the Toca Development Kit (TDK), an all-in-one integrated development environment (IDE) that's accessed via a single web interface. You can access the TDK by prefixing the Toca platform URL with `ui-tdk`. For example, if the toca platform URL is `https://trial.toca.cloud` then the TDK associated with this platform can be reached at `https://ui-tdk.trial.toca.cloud`.

The TDK allows you to edit existing actions and app components as well as add new ones to the platform. The TDK contains all the necessary tools required to quickly develop new features and integrate them into the main Toca platform, making them available to everyone using the platform.

Where the Automation projects and App projects champion the use of no code so you can make progress quickly and practically, the TDK is a high code tool as sometimes there is no substitute for writing code. By making the TDK a high code tool, the possibilities for new features are virtually limitless. 


![TDK Home Screen](https://lh4.googleusercontent.com/W6vVE1TxYJJ5v6jbmQHOkkCrqJ875bwMZq8n4LqHgPJH-1JmedLwNXmq21d8sjfakEdy7-XFYxfmR9TBMaJgtzCl2yTyoDXV20Mwo-Xre-gh3iWGhjKm2Ja4ehOE0o2Fbwc1osZ2) 


#### How is it organised?

The TDK is split into 5 parts:

- Actions - edit or create actions to suit your automation needs
- Action Groups - Add your new actions to an action group or create a new one, Action Groups are how the actions are organised into categories in the Activity Designer
- Action Packs - An action pack is useful if you wish to share your new actions with the rest of the world by uploading them to a Hub.
- Action Helpers - Extract any commonly used functionality to Helper classes which you can use in any action
- App Components - Edit or create app components to help create the Apps you want.

Each of these parts has their own space in the TDK but Action Groups and Packs do not have a development environment as those parts do not involve any development. For these parts you simply drag and drop the actions you want in your group or drag the group you want in your action pack.
Actions, Action Helpers and App components each have their own development environment tailored specifically for what you are developing.

#### Who is it for?

The TDK is primarily aimed at developers or those with a technical background who aren't afraid to roll up their sleeves and take a look under the bonnet. There are currently two languages which you can use in the TDK:


- C# (.NET 6) for developing actions and action helpers.
- TypeScript/JavaScript for developing App components in the React framework.

There are plans to introduce Python as well for action development to open up the TDK to a wider audience, stay tuned for this.
It is also worth mentioning that all the actions on the platform were made using the TDK by the developers behind Toca so it is a tried and tested method!
 
## Requirements

#### Browser Requirements

The TDK is a cloud-based development environment, it is designed to run in your browser on any modern full desktop operating system. The following browsers are supported:

- Chrome (for the best experience)
- Firefox
- Edge

  > **Note:** Internet Explorer is _NOT_ supported.
