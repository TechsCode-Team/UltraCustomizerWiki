### Example Element Code
The "Get Item In Slot" element from inventory utils.
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
