
# TDK Actions



 
Actions are the backbone of automation within Toca so let's take a look at how an action is made. We'll look at an example of adding an action which lets us add a unit of time (days, hours, minutes or seconds) to the current time.

#### Create/Edit an action

To access the TDK prefix the Toca platform url with *ui-tdk.* so if the URL was "*trial.toca.cloud"* then it would become "*ui-tdk.trial.toca.cloud"*. You will be prompted to log into the TDK,  as long as your Toca user has the TDK role then you should be able to login using your Toca user. When you log in you'll be greeted with a homepage that looks like this:




![Image](https://lh3.googleusercontent.com/ylW84bIj80J5KEB3FkqlrGhoUpJDS8YPusl9vsVcNeoWZNFP6jRL8_nMh2dAuzP62XyNLRmFwzti97JYPoMbK5lSvFgmDGfQW4InAhubwSC90BZS0k4bLdBb1c7S7K_QEQKEneF0) 

To create a new action let's click on CREATE ACTION.

![TDK actions 2](https://docs.toca.io/hs-fs/hubfs/TDK%20actions%202.png?width=394&name=TDK%20actions%202.png) 

A window will appear asking for a name and keyname for the action, the keyname is how the action is identified behind the scenes whilst the name is what the user sees.

![Image](https://lh4.googleusercontent.com/egqWBskG7MBde-madB7Ch-DG3l4shuAK1oisfGss0nlkCgiMOCFxSLTbXu_JVseHyavSivWHV1aHB2ccleFQplo3k1htdeBTOQjsvNUxKvsMgIawznVioN2QciX5AlLsNQcS0337) 

The window also has a property called *Can have children?* This refers to whether or not this action should expect one or more actions to be nested underneath it. In our example the action does not expect actions to be nested underneath it so we can leave this unticked. Let's finish up by giving the action a key of *ModifyTime* and a name of *Modify Time*. Click CREATE when all the details are filled in.




![TDK actions 4](https://docs.toca.io/hs-fs/hubfs/TDK%20actions%204.png?width=439&name=TDK%20actions%204.png) 

This will take you to the Action IDE which will look similar to this:

![Image](https://lh5.googleusercontent.com/nfkOq1cRlID3PbVVG3rI1mu4hGzJthUHJGsvhAc4Z4p5C16x8v7WpJOtyTsm-mkt-Ma5ffxYh6ONZQspvfG0fbu8lNoTxHQX5R20C2q5epU6xZsqfhyGKe2FETsFG0gleQls1tG9) 

You have UI controls on the left (you'll learn about these in the next section of the chapter), inputs/outputs and code in the middle and a Bot screen on the right (more on this in the *Upload a draft action* section in this chapter).

Let's focus on writing the code first.

![Image](https://lh6.googleusercontent.com/o7xnp7SXZX71Knu90scs8hI0MUYuvcl63lxrC9D5G94at9bF5CF-mngYu9jF2O9H9-2g1f7ogv1Gf5D4n-z8owdAO_XXAOmMZFS9ElfOHN-0CFDqNvq7DOxFvV5Oa7Wunhb70WJX) 

This will do for now, although in future you could extend it to allow users to add months or years to the current date.
You may have noticed that inside that code snippet there are two variables called *unit* and *valueToAdd* which aren't initialised or declared anywhere; so where did they come from?


Well, the answer is that they get injected into your action code as they come from user inputs. Let's have a look at how to add user inputs next.

#### UI Controls

The UI Controls are what let's a user add values to an action when they place it down on the action palette in the Activity Designer. They appear on the left of the Action IDE.

![Image](https://lh6.googleusercontent.com/85A48wvPH_iFZjDJ3hGqdsduL3QZ8HNkWsrBsq6idE2fqoLosKhnRJxqSe7_hh7fX1fE_H4tDcrXuCNgodU4hojZmwbhNulEvlyLOT4P4drkFjNniyFqhEeE-ucsH0wz1iPFnmYf) 

You simply need to find the controls that you need for your action and drag them in. For our action we want two different controls:


- A dropdown list letting a user select what unit of time they wish to modify the current datetime by


- A number field that lets the user define what value to modify the date by

We'll drag in the dropdown first.

![TDK actions 8](https://docs.toca.io/hs-fs/hubfs/TDK%20actions%208.png?width=356&name=TDK%20actions%208.png) 

Now we have dragged in the dropdown we can configure it, you do this by clicking on the cog icon next to the control.

![TDK actions 9](https://docs.toca.io/hs-fs/hubfs/TDK%20actions%209.png?width=343&name=TDK%20actions%209.png) 

The properties for this dropdown control will at first be empty.

![Image](https://lh6.googleusercontent.com/QhY-XdtiGHBGhj3T39H77sJj5h8AfjwEM0UMLCS0AijcbRIv3BMSUHM6dlIlwagxHjRwy_NBJgYjqW-QUFKeqEa0CiAqaE-SNQlfq_u-ZttOTaVXw03LfARmC04xUHp3fAbcWRdc) 

Let's define some properties. The first one is the Parameters property, this is the name given to the variable which represents the users input on this control. We'll give it the parameter value of *unit* as we have already called this variable *unit* in our code.


Next we define the Label which is the name given to the field that the user will see; we could give it the label of *Unit of time.* Now we can start adding items to our dropdown. When you add items there are two fields per item: the name of the item which is what the user will see (and then the value which the name maps to), the value is what the code will receive.


![Image](https://lh6.googleusercontent.com/LEMd5wewZBv_qWk_l5puOtzxU4ZkxOdYNEqIlYBsEVeGOjU_q0pbiRH5nO-BS2_HnNON5hJjkFomvavzF-fCf0eGlepu5s-pvJTW01dtWEAfvnMtFaLhJElBWEJQpi9brXeiSOVj) 

That's the first input sorted, now let's add a number control so the user can specify the value to modify the time by and configure it appropriately.

![Image](https://lh3.googleusercontent.com/Cwq1MPqwOsCclTfBl4LtlH0L_2Z_pBIdSON3f3oqyia3uQWU8WVU2b_REZ1JBOGoZocrDLn3but4EwJD5zk9lIFzs4nFcoUuGrMhjNnHTaDU1gkDU6fB8JQSJKnl-oVQlLxVBBkm) 

As you add user controls you'll notice that they begin to appear as inputs above the code.

![TDK actions 13](https://docs.toca.io/hs-fs/hubfs/TDK%20actions%2013.png?width=602&name=TDK%20actions%2013.png) 

 
We can preview what the action will look like by clicking the eye icon on the controls panel.

![TDK actions 14](https://docs.toca.io/hs-fs/hubfs/TDK%20actions%2014.png?width=394&name=TDK%20actions%2014.png) 

This will not also let you use the inputs to check everything appears as it should.

![Image](https://lh4.googleusercontent.com/nMzin77V4cJ4V0c_MYde5asVBp74XjnFFvxOYSDgKVTH6cImYvzomp8QJZPVVJwZRQwb2Jir5zxn4JLPlmiOOWhjS3oFzpZHfPOzuEWtYR6AkIMCwkucYyRoYuqAvn9YVsF8kWan) 

We can test the dropdown list contains what we expect by clicking on the dropdown.

![Image](https://lh5.googleusercontent.com/1VTLS41rzqjHO88_vwY7G8ZmDqUOAty1Nt9Y7K_RLBsrjH2ZU5txaIHyG-V8UiKQeRc4qUUfw9NALHJkFvs5IG0j4L2qEA_Y9BSHuzXO80ytjzVD5f41UCAHZ0GXE5IBtvg64KW1) 

Great! Now what if we want to test the action before we release it? That's where draft actions come to the rescue.

#### Upload a draft action

On the right hand side of the Action IDE there are some settings which allow you to connect a bot to the development environment so you can test your action.

![TDK actions 17](https://docs.toca.io/hs-fs/hubfs/TDK%20actions%2017.png?width=300&name=TDK%20actions%2017.png) 

Click on the cog to select a Bot, make sure you have at least one bot associated with your user first.

![Image](https://lh6.googleusercontent.com/EAvQUnCgMxy4AEpb5KVZaLSZMq4rUxPteFet91_yYJU0SsD0rI-BwR0bXVcS7cbc9dyR125Zuf-1J4etBz9s3E2KCsT3s_zq7WmH2Pffj_oYgOAJn66k30vooCeDFGlc3lVtF78w) 

Once you have selected your Bot you can upload your action as a draft to the Bot to check the code you have written works and the action does what you expect it to.
Save your action and click the upload button on the right hand side of the top bar.

![TDK actions 19](https://docs.toca.io/hs-fs/hubfs/TDK%20actions%2019.png?width=317&name=TDK%20actions%2019.png) 

Provided the code that was written is correct, your action should upload successfully to the Bot and you'll get a notification informing you of that.

![Image](https://lh6.googleusercontent.com/GTVnum8841b-hMiQvG3Jv6ZF_PLwhMMe2oIvSZg2fengJuV3kspFz6z5BgTwxCOCExZp0GgdU8t-V62-hk-0UziLLoEBSZtd_qMpU7QuZDSCOzMX2jE4SLPiSA0P7VxyQ6mfl36a) 

If your code does not compile then you'll receive an error message informing you of the cause which is useful for debugging your code.
Not if you open an activity in the Activity Designer which uses this Bot you'll notice a new action category on the action panel.

![TDK actions 21](https://docs.toca.io/hs-fs/hubfs/TDK%20actions%2021.png?width=478&name=TDK%20actions%2021.png) 

Click on the TDK category and you'll see your new Modify Time action.

![Image](https://lh3.googleusercontent.com/eCb3JFpg0vyltebuzhQZVJBkMuo2IpTeZx1rMxN6c53ce6yu6VuoDx4Wk_bPHWHiUEtGlGCYfpgb7Dz60uBtJgCXifpiZ3je6gCnKDvHJx4keuohLsWu2lGOpkQXfBHklfyaPBQT) 

Let's try using the new action.

![Image](https://lh5.googleusercontent.com/51K1g611PE_4NOf4vXddLVb3OkVAJfw9g33u0F3g_7mkkgWoASTibAoXp384YKCOG6GSqtyN5iP6P1n_KxRFQQQKpEUhVumdG-A330VOki78PSnyZgY6P4glkXLE5my7ocOlSbB4) 

Have a play with the properties and then run the action and check the console to see if the output is what you expected.

![Image](https://lh4.googleusercontent.com/1CHcqhPzEj1XQAD_8w1JVJhQ6GmDAEGeezi3ucAWh8OsgoF2CVOErS3fuRIpfCob9rE8sCyi5vOm_Lr0z5Ft6pVCihA314I1h__X6ZvOMevPR5VDwcNuJoUgWp3Cu7mCQDVNdQN6) 

If you run the action with these properties then it should return what the time was half an hour ago.

![TDK actions 25](https://docs.toca.io/hs-fs/hubfs/TDK%20actions%2025.png?width=602&name=TDK%20actions%2025.png) 

That looks correct, so now we've tested the action we can publish it to make it available to everyone!
 

#### Publishing an action

You publish an action from the Action IDE in the TDK. In the top right hand corner there is a publish button.

![TDK actions 26](https://docs.toca.io/hs-fs/hubfs/TDK%20actions%2026.png?width=292&name=TDK%20actions%2026.png) 

When you publish an action it will be sent for review first instead of being published straight to the platform. 

#### Reviewing an action

When an action is sent for review it must be reviewed by someone else on your Toca platform, you cannot approve actions that you have sent for review. It only requires one other user to approve it and then once approved it will automatically be published to the platform.

![TDK actions 27](https://docs.toca.io/hs-fs/hubfs/TDK%20actions%2027.png?width=488&name=TDK%20actions%2027.png) 

When reviewing an action you can test it or modify it.

![Image](https://lh5.googleusercontent.com/CMz6UBmB66edu3Asdxb9xM5giSvTCmll2Q4D5NGpgbeceFLTntuBgqJYeVAi-iphZfbEBtF_XAkzsvL0Btnh_fnWPLTKxcgIX4JYpA-haa77tnGyQJsiY8CfRrOAfIGWYe17OdFN) 

Here the Modify Action might be rejected as it does not have an icon for the action, if an action is rejected you must provide a reason so that whoever submitted the action for review knows what to change to get it approved.

![Image](https://lh6.googleusercontent.com/3K0q-F3tztfthaqxHR5py7t_rc1FP5L9s21dVCQpYTJJz9EwmxjIDCmozcXTP2ljgVBbxlMA4hLcALjB6wbY4qWT2WwhfrOrq4My7B8hTXXo6Ij1tAGEkajDzio5xN8eD0nRxSBI) 









#### Action Groups

Once an action has been approved you can add it to an action group. An action group is simply a way of grouping similar actions and the groups are what are displayed in the Activity Designer. There is already a DateTime action in the Advanced group so the Modify Time action might be best placed in the advanced group.
 
Simply drag the new action into the group and then save the action group.

![Image](https://lh4.googleusercontent.com/lI8aY5O7Sr5kJunDencTygDKNcw343KBTqph0PrUff5-8NYV6JkqvbSIc1a1QubYkBuyefFR0gFcTDyZRwMWWjgT8xZpTYq_EhH09_VbRkylM0KxPPVDqV8LomVCWF3NXLs7lwyK) 

 

#### Action Packs

If you wish to publish your new action to the wider world so other users on other Toca platforms can use your action then you need to add the action to an Action Pack and publish the action pack to the Hub. An Action Pack consists of a collection of action groups which can contain one or more actions.

![Image](https://lh5.googleusercontent.com/_OIruISY9Hy-iOzfrWI5fAjL9RflRe-h4rgCmJc1gCL3AlSG69dbqd6k5w-waQPIgz-drpkStx3ZSW15jdxDDviCYwaj5B4Kx7DndeAsDyz1FDsxWxOBfstEh3eT1tIJgFmEWT8v) 

 
Simply drag in the groups you want to include in your action pack and then select the actions within each group you want to include. When you are happy with the action pack you have created/modified then save your changes and click publish. Both the save and publish buttons can be found in the top right corner of the action pack page.

![TDK actions 32](https://docs.toca.io/hs-fs/hubfs/TDK%20actions%2032.png?width=227&name=TDK%20actions%2032.png) 

When you publish your pack you'll be prompted to give it a version number so any future changes can be distinguished through different versions.

![Image](https://lh3.googleusercontent.com/d9CU9aDr0ufTFV_veYKj-SXlwMtF9L42l7NAUbUvQcIp2SOi2scfl8cLHnxr731-ZFqgW7Rjk--eOVF-iwwCOVNxnsK332kMIYsANPb80NXOtaEv30r8Wg8RPg-IWzOYUGC-ck-6) 

Once you have published the Action Pack it will be available for anyone to download onto their Toca platform and use.
 
