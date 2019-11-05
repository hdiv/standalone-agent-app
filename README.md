# Standalone Agent App
This is an empty Spring Boot application. It can be used to run the Hdiv Agent in remote so it can be used 
from a web page or application (from now, client application) to detect Untrusted Client Access attacks.

## Run the Standalone Agent App
It's an Spring Boot application, so it can be executed form an IDE (ideally, Spring Tool Suite) or 
from the command line. 

Add the Hdiv Agent location adding the following line under VM arguments

* -javaagent:{path-to-hdiv-folder}/hdiv-ee-agent.jar

Add the following options using Java system properties for a proper execution of the agent. 

* hdiv.console.url: Url of the Hdiv Console application.
* hdiv.console.token: Token of the environment in the Hdiv Console associated with the client application.
* hdiv.server.name: Name of the server that runs the client application.
* hdiv.config.dir: Path to the directory where the Hdiv license is present.
* hdiv.base.internal.url: Base path to get the script file form the Hdiv Agent.
* hdiv.multiple.filter: Set this property to true to use the Context Path of the script file as the 
name of the client application.

Add other configuration options for the Java Agent if its needed

## Use the Standalone Agent App from the Client Application
To use the agent through the standalone agent app from a client application, you must include a javascript 
file of the agent in every page that must be analyzed. This reference must be the first javascript file included
in the page.

The script tag used must have these form

<script src="http://${SERVER}:${PORT}/${APP}/${CONTEXT}/uca/static/${FILENAME}.js" type="text/javascript" ></script>

where

* ${SERVER}: Name of the server that runs this application.
* ${PORT}: Port of the server where this application runs.
* ${APP}: Name of the client application.
* ${CONTEXT}: Value of the property hdiv.base.internal.url.
* ${FILENAME}: Name of the file. It can take any value

For example

<script src="http://scripts.demo.com:8480/app/analyzers/uca/static/hdiv-name-could-be-changed.js" type="text/javascript"></script>
