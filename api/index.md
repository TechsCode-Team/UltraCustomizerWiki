## Usage
The API of **Ultra Customizer** can be used to make addons for the marketplace. To use the API the Ultra Customizer jar and the Spigot jar must be added to the library of the workspace. Your main class should extend `Constructor` for construcors and `Element` for elements.
<br>

## Initialization
To make the element work the you first have to add the following code:
```java
public ClassName(UltraCustomizer plugin) {
	super(plugin);
}
```
This is the same for both elements and constructors.
<br>

## Get Name
The next thing to add is the element or constructor name.
```java
public String getName() {
	return "Element Name";
}
```
<br>

## Get Internal Name
Afterwards you will want to set the name the plugin views the element as. This name can not have spaces and should not have capitals.
```java
public String getInternalName() {
	return "element-name";
}
```
<br>

## Hiding if not Compatible
Here you will input this code. Do not change it unless you know what you are doing.
```java
public boolean isHidingIfNotCompatible() {
	return false;
}
```
<br>

## Get Material
This will return the material the element or constructor will have.
```java
public XMaterial getMaterial() {
	return XMaterial.BARRIER;
}
```
<br>

## Get Description
This will get the description your element or constructor will have in the selection gui.
```java
public String[] getDescription() {
	return new String[] { "Lore Description" };
}
```
You can add multiple lines by adding a comma between the lines. EX: `{ "Lore1", "Lore2" }`.
<br>

## Get Arguments
This will be the arguments that the user is prompted to put in.
<br>

### No Arguments
```java
public Argument[] getArguments(ElementInfo elementInfo) {
	return new Argument[0];
}
```
### With Arguments
```java
public Argument[] getArguments(ElementInfo elementInfo) {
	return new Argument[] { new Argument("internal-name", "Display Name", DataType.PLAYER, elementInfo) };
}
```
You can add multiple arguments adding a comma and repeating the new argument code `new Argument("internal-name", "Display Name", DataType.PLAYER, elementInfo)`.
<br>

### Avalible Datatypes
<br>

* Arguments
* Block
* Boolean
* Cancellable Event
* Click Type
* Interface
* Item
* Material
* Number
* Player
* Sound
* String
* Ticks
* Time
<br>

## Outcoming Variables
This will be the variables the element creates which can be used by other elements.
<br>

### No Variables
```java
public OutcomingVariable[] getOutcomingVariables(ElementInfo elementInfo) {
	return new OutcomingVariable[0];
}
```
### With Arguments
```java
public OutcomingVariable[] getOutcomingVariables(ElementInfo elementInfo) {
	return new OutcomingVariable[] { new OutcomingVariable("internal-name", "Display Name", DataType.PLAYER, elementInfo) };
}
```
You can add multiple arguments adding a comma and repeating the new argument code `new OutcomingVariable("internal-name", "Display Name", DataType.PLAYER, elementInfo)`.
<br>

### Avalible Datatypes
<br>

* Arguments
* Block
* Boolean
* Cancellable Event
* Click Type
* Interface
* Item
* Material
* Number
* Player
* Sound
* String
* Ticks
* Time
<br>

## Get Connectors
This will go to the next element after this element is complete. **Only for elements, not constructors**.
```java
public Child[] getConnectors(ElementInfo elementInfo) {
	return new Child[] { (Child) new DefaultChild(elementInfo, "next") };
}
```
<br>

## Run
This is where you will run your desired code for elements.
```java
public void run(ElementInfo info, ScriptInstance instance) {

	Player p = (Player) getArguments(info)[0].getValue(instance);
	int n = (int) (long) getArguments(info)[1].getValue(instance);
  
  Your code here (code that does not affect outcoming variable)

	getOutcomingVariables(info)[0].register(instance, new DataRequester() {
		public Object request() {
    
    Your code here
    
		}
	});

	getConnectors(info)[0].run(instance);

}
```
### Using Arguments
In order to use the value of the incoming arguments, you have to use `getArguments(info)[0].getValue(instance)`, with the number being equal to argument in the order added.
<br>

## Setting Outcoming Variable
To set the outcoming variable you have to use
```java
	getOutcomingVariables(info)[0].register(instance, new DataRequester() {
		public Object request() {
		}
	});
```
Inside the public Object request is where you will execute code to set the variable, using `return (value)` to set the outcoming variable.
<br>

### No Outcoming Variable
When there is no outcoming vaiable ignore the above step, and just execute the code in the run function.
<br>

## Event Handler
For constructers this is what will listen for a minecraft event that elements will run off. To find what events you can listen for check the spigot javadocs.
```java
@EventHandler(priority = EventPriority.LOWEST)
public void ClassName(EventToListenFor e) {
		call(e);
}
```
<br>

## Preventing Errors
To prevent errors you can use a if statements to check if variables you are using are null, and only calling your code when the item is not. For example:
```java
if (e.getItem() != null)
	call(e);
```
This will only call the event if the item used in the event is not null. Useful when you use variables which break when null.
<br>

## Call
This is the code that will be executed in constructures when the event is called.
```java
public void call(final SameEventAsEventHandler e) {
	call(elementInfo -> {
		ScriptInstance instance = new ScriptInstance();
		getOutcomingVariables(elementInfo)[0].register(instance, new DataRequester() {
			public Object request() {
				return e;
			}
		});
		return instance;
	});
}
```
Here is where you will set the values for the outcoming vairbales. The first is an example for setting the Cancelable event variable.
<br>

## Is Unlisted
Weather or not the constructor is listed or not.
```java
public boolean isUnlisted() {
	return false;
}
```
<br>

### Example Element Code
The "Get Item In Slot" element from Inventory Utils.
```java
import org.bukkit.Material;
import org.bukkit.entity.Player;
import org.bukkit.inventory.ItemStack;

import me.TechsCode.UltraCustomizer.UltraCustomizer;
import me.TechsCode.UltraCustomizer.base.item.XMaterial;
import me.TechsCode.UltraCustomizer.scriptSystem.objects.Argument;
import me.TechsCode.UltraCustomizer.scriptSystem.objects.Child;
import me.TechsCode.UltraCustomizer.scriptSystem.objects.DataRequester;
import me.TechsCode.UltraCustomizer.scriptSystem.objects.DefaultChild;
import me.TechsCode.UltraCustomizer.scriptSystem.objects.Element;
import me.TechsCode.UltraCustomizer.scriptSystem.objects.ElementInfo;
import me.TechsCode.UltraCustomizer.scriptSystem.objects.OutcomingVariable;
import me.TechsCode.UltraCustomizer.scriptSystem.objects.ScriptInstance;
import me.TechsCode.UltraCustomizer.scriptSystem.objects.datatypes.DataType;

public class GetItemInSlot extends Element {
	public GetItemInSlot(UltraCustomizer plugin) {
		super(plugin);
	}

	public String getName() {
		return "Get Item In Slot";
	}

	public String getInternalName() {
		return "get-item-in-slot";
	}

	public boolean isHidingIfNotCompatible() {
		return false;
	}

	public XMaterial getMaterial() {
		return XMaterial.CHEST;
	}

	public String[] getDescription() {
		return new String[] { "Get the item in a specific inventory slot" };
	}

	public Argument[] getArguments(ElementInfo elementInfo) {
		return new Argument[] { new Argument("player", "Player", DataType.PLAYER, elementInfo),
				new Argument("slot", "Slot", DataType.NUMBER, elementInfo) };
	}

	public OutcomingVariable[] getOutcomingVariables(ElementInfo elementInfo) {
		return new OutcomingVariable[] { new OutcomingVariable("item", "Item", DataType.ITEM, elementInfo) };
	}

	public Child[] getConnectors(ElementInfo elementInfo) {
		return new Child[] { (Child) new DefaultChild(elementInfo, "next") };
	}

	public void run(ElementInfo info, ScriptInstance instance) {

		Player p = (Player) getArguments(info)[0].getValue(instance);
		int n = (int) (long) getArguments(info)[1].getValue(instance);

		getOutcomingVariables(info)[0].register(instance, new DataRequester() {
			public Object request() {

				if (p.getInventory().getItem(n) != null) {

					return p.getInventory().getItem(n);

				}
				ItemStack item = new ItemStack(Material.AIR);
				return item;
			}
		});

		getConnectors(info)[0].run(instance);

	}
}
```

### Constructor Example Code
From the "Item Move Event" constructor in Inventory Utils.
```java
import org.bukkit.Material;
import org.bukkit.event.EventHandler;
import org.bukkit.event.EventPriority;
import org.bukkit.event.inventory.InventoryMoveItemEvent;
import org.bukkit.inventory.ItemStack;

import me.TechsCode.UltraCustomizer.UltraCustomizer;
import me.TechsCode.UltraCustomizer.base.item.XMaterial;
import me.TechsCode.UltraCustomizer.scriptSystem.objects.Argument;
import me.TechsCode.UltraCustomizer.scriptSystem.objects.Constructor;
import me.TechsCode.UltraCustomizer.scriptSystem.objects.DataRequester;
import me.TechsCode.UltraCustomizer.scriptSystem.objects.ElementInfo;
import me.TechsCode.UltraCustomizer.scriptSystem.objects.OutcomingVariable;
import me.TechsCode.UltraCustomizer.scriptSystem.objects.ScriptInstance;
import me.TechsCode.UltraCustomizer.scriptSystem.objects.datatypes.DataType;

public class ItemMove extends Constructor {
	public ItemMove(UltraCustomizer UltraCustomizer) {
		super(UltraCustomizer);
	}

	public String getName() {
		return "Item Move Event";
	}

	public String getInternalName() {
		return "item-move-event";
	}

	public XMaterial getMaterial() {
		return XMaterial.ITEM_FRAME;
	}

	public Argument[] getArguments(ElementInfo elementInfo) {
		return new Argument[0];
	}

	public String[] getDescription() {
		return new String[] { "Will be executed when an item is", "moved from one inventory to another.",
				"EX: Item moving to a hopper." };
	}

	public OutcomingVariable[] getOutcomingVariables(ElementInfo elementInfo) {
		return new OutcomingVariable[] {
				new OutcomingVariable("event", "Event", DataType.CANCELLABLE_EVENT, elementInfo),
				new OutcomingVariable("item", "Moved Item", DataType.ITEM, elementInfo),
				new OutcomingVariable("source", "Source Inventory", DataType.STRING, elementInfo),
				new OutcomingVariable("destination", "Destination Inventory", DataType.STRING, elementInfo) };
	}

	@EventHandler(priority = EventPriority.LOWEST)
	public void onItemMove(InventoryMoveItemEvent e) {
		if (e.getItem() != null)
			call(e);
	}

	public void call(final InventoryMoveItemEvent e) {
		call(elementInfo -> {
			ScriptInstance instance = new ScriptInstance();
			getOutcomingVariables(elementInfo)[0].register(instance, new DataRequester() {
				public Object request() {
					return e;
				}
			});
			getOutcomingVariables(elementInfo)[1].register(instance, new DataRequester() {
				public Object request() {
					ItemStack i = new ItemStack(Material.AIR);
					return (e.getItem() == null) ? i : e.getItem();
				}
			});
			getOutcomingVariables(elementInfo)[2].register(instance, new DataRequester() {
				public Object request() {
					return e.getSource().getType().toString();
				}
			});
			getOutcomingVariables(elementInfo)[3].register(instance, new DataRequester() {
				public Object request() {
					return e.getDestination().getType().toString();
				}
			});
			return instance;
		});
	}

	public boolean isUnlisted() {
		return false;
	}
}
```
<br>

## addon.yml File
You need an addon.yml in order to convey 3 important peices of info about the plugin; who made it, what version the addon is, and its name.

```java
name: AddonTest
version: 1.0.0
author: MeepTortoise
```

*Make sure the version is x.x.x and the name matches the jar file name and the upload name*
