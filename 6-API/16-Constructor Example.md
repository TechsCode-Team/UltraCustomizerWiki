### Constructor Example Code
From the "Item Move Event" constructor in inventory utils.
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
	public ItemMove(UltraCustomizer ultraCustomizer) {
		super(ultraCustomizer);
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
