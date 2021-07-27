### Run
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
### Setting Outcoming Variable
To set the outcoming variable you have to use 
```java
	getOutcomingVariables(info)[0].register(instance, new DataRequester() {
		public Object request() {
		}
	});
  ```
  Inside the public Object request is where you will execute code to set the variable, useing `return (value)` to set the outcoming variable.
  ### No Outcoming Variable
  When there is no outcoming vaiable ignore the above step, and just execture the code in the run function.
