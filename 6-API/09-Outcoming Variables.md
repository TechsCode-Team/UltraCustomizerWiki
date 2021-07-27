## Outcoming Variables
This will be the variables the element creates which can be used by other elements.
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
### Avalible Datatypes
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
