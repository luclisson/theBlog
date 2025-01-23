

all of the different dependencies which are added to your [[spring boot starter projects]] need to be configured. As said there are many dependencies. spring boot auto configuration simplifies that process.

the automated config will be created based on which frameworks are in your class path (which class path). those frameworks are provided by the starter projects.

- configured in the maven dependencies folder as "spring-boot-autoconfigure-...jar"