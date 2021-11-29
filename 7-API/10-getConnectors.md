### Get Connectors
This will go to the next element after this element is complete. **Only for elements, not constructors**.
```java
public Child[] getConnectors(ElementInfo elementInfo) {
	return new Child[] { (Child) new DefaultChild(elementInfo, "next") };
}
```
