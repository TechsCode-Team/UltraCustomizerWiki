### Event Handler
For constructers this is what will listen for a minecraft event that elements will run off. To find what events you can listen for check the spigot javadocs.
```java
@EventHandler(priority = EventPriority.LOWEST)
public void ClassName(EventToListenFor e) {
		call(e);
}
```
### Preventing Errors
To prevent errors you can use a if statements to check if variables you are using are null, and only calling your code when the item is not. For example:
```java
if (e.getItem() != null)
	call(e);
```
This will only call the event if the item used in the event is not null. Useful when you use variables which break when null.
