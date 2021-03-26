### Call
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
