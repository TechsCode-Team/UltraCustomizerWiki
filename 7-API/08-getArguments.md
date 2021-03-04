## Get Arguments
This will be the arguments that the user is prompted to put in.
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
