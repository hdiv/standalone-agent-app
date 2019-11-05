# Standalone Agent App
This is an empty Spring Boot application. It can be used to run the Hdiv Agent in remote so it can be used 
from a web page or application (from now, client application) to detect Untrusted Client Access attacks.

## Run the Standalone Agent App
It's an Spring Boot application, so it can be executed form an IDE (ideally, Spring Tool Suite) or 
from the command line. 

Add the Hdiv Agent location adding the following line under VM arguments

```
-javaagent:{path-to-hdiv-folder}/hdiv-ee-agent.jar
```

For example

```
-javaagent:/Users/develop/hdiv/hdiv-ee-agent.jar
```

Add the following options using Java system properties for a proper execution of the agent. 

* **hdiv.console.url**: Url of the Hdiv Console application. By default, [http://localhost:8089/hdiv-console-web](http://localhost:8089/hdiv-console-web)
* **hdiv.console.token**: Token of the environment in the Hdiv Console associated with the client application. For example
**6a367E2eb97db59020a47340**
* **hdiv.server.name**: Name of the server that runs the client application. For example, **Test-Server**
* **hdiv.config.dir**: Path to the directory where the Hdiv license is present. For example, **/Users/develop/hdiv/**
* **hdiv.base.internal.url**: Base path to get the script file form the Hdiv Agent. The suggested value is **assets**
* **hdiv.multiple.filter**: Set this property to **true** to use the Context Path of the script file as the 
name of the client application.

For example

```
-javaagent:/Users/develop/hdiv/hdiv-ee-agent.jar
-Dhdiv.console.url=http://localhost:8089/hdiv-console-services 
-Dhdiv.console.token=6a367E2eb97db59020a47340 
-Dhdiv.server.name=Test-Server 
-Dhdiv.config.dir=/Users/develop/hdiv/
-Dhdiv.base.internal.url=assets
-Dhdiv.multiple.filter=true
```

Add other configuration options for the Java Agent if its needed

To run the application from the command line, first compile the application with the command

mvn clean install

Then, run the application with a command similar to this, changing the values of the properties for the real values

```
java -javaagent:/Users/develop/hdiv/hdiv-ee-agent.jar -Dhdiv.console.url=http://localhost:8089/hdiv-console-services  -Dhdiv.console.token=6a367E2eb97db59020a47340  -Dhdiv.server.name=Test-Server  -Dhdiv.config.dir=/Users/develop/hdiv/ -Dhdiv.base.internal.url=assets  -Dhdiv.multiple.filter=true -jar target/standalone-agent-app-0.0.1-SNAPSHOT.jar 
```


## Use the Standalone Agent App from the Client Application
To use the agent through the standalone agent app from a client application, you must include a javascript 
file of the agent in every page that must be analyzed. This reference must be the first javascript file included
in the page.

The script tag used must have these form

```
<script src="http://${SERVER}:${PORT}/${APP}/${CONTEXT}/uca/static/${FILENAME}.js" type="text/javascript" ></script>
```

where

* **${SERVER}**: Name of the server that runs this application. For example, **scripts.demo.com**.
* **${PORT}**: Port of the server where this application runs. For example, **8080**
* **${APP}**: Name of the client application. For example, **myapp**
* **${CONTEXT}**: Value of the property **hdiv.base.internal.url**. The suggested value for this property is **assets**
* **${FILENAME}**: Name of the file. It can take any value, for example, **main.js**

For example

```
<script src="http://scripts.demo.com:8080/myapp/assets/uca/static/main.js" type="text/javascript"></script>
```