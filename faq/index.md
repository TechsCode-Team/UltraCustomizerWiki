# Overview
Below you can find all the frequently asked questions of Ultra Customizer. If your question is not in here feel free to ask it in the **[Discord](https://discord.gg/3JuHDm8)**
<br>

## Frequently Asked Questions of Ultra Customizer
<br>

Here are all the frequently asked questions from Ultra Customizer.
<br>

* **`How can i make suggestions?`**
  You can make suggestions at our [feedback repository](https://github.com/TechsCode-Team/Feedback/discussions/categories/suggestions)
* **`Can i use custom model data item?`**
  Yes, you can use custom model data item as buttons
* **`Is there any guide to learn how to use Ultra Customizer?`**
  Yes, you can find a guide for learn how to use Ultra Customizer **[HERE](https://guides.ultracustomizer.com/)**
* **`I lose my GUIs and Commands if i update the plugin?`**
  No, you don't lose any data if you properly update the plugin
* **`How can I access a custom menu or command from another seperate folder?`**
<br>

  This isn't really supported as folders are supposed to be seperate from each other, however here is an example of a work around; 
<br>
  Player has custom command/menu X sitting inside folder A. Player makes another custom command inside folder B, if the player wants this custom command from   folder B to open menu X from folder A, they can set the custom player command element to `/interface menuX`. Alternativly, you can install the [Essentials]   (https://www.spigotmc.org/resources/9089/) plugin and utilize the `sudo` command. Start by getting the player name element, followed by the console command   element with `sudo %1 customCommandFromFolderA` which will run your `customCommandFromFolderA` as the player. The vanilla `execute` command also has similar  functionality to the essentials `sudo` command, but it seems to only allow vanilla commands in its arguments.
