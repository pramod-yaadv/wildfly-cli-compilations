# wildfly-cli-compilations (standalone mode)
This is the repository for useful Wildfly cli commands to perform or manage Wildlfly in Runtime. Currently Only release standalone mode commands and later will update on domain mode.

## Index
- Enable Datasource Stats 
- See statistics
- List all available datasources
- Write, remove attributes
- DataSource
- Flush datasources
- HTTP Configuration
- List Subsystems
- To get interface address
- Add a log category
- Graceful Shutdown [Start / Shutdown/ Suspend / Resume]
- View all system properties
- All Operations List
- Add, read, remove, write- System attribute


## Enable Datasource Stats 
/subsystem=datasources/data-source=ecommDS/statistics=pool:write-attribute(name=statistics-enabled,value=true)
/subsystem=datasources/data-source=ecommDS/statistics=jdbc:write-attribute(name=statistics-enabled,value=true)
/subsystem=datasources/data-source=ecommDS:write-attribute(name=statistics-enabled,value=true)

## See statistics
/subsystem=datasources/data-source=ecommDS/statistics=pool:read-resource(include-runtime=true)
/subsystem=datasources/data-source=ecommDS/statistics=jdbc:read-resource(include-runtime=true)
/subsystem=datasources/data-source=ecommDS:read-resource(include-runtime=true,recursive=true)

## List all available datasources
/subsystem=datasources:read-resource

# Write, remove attributes
/subsystem=datasources/data-source=ecommDS:write-attribute(name=query-timeout,value=300)
/subsystem=datasources/data-source=ecommDS:undefine-attribute(name=query-timeout)

# DataSource
/subsystem=datasources/data-source=ecommDS:test-connection-in-pool()
/subsystem=datasources/data-source=ecommDS/statistics=pool:read-resource(include-runtime=true)
/subsystem=datasources/data-source=ecommDS/statistics=jdbc:read-resource(include-runtime=true)
/subsystem=datasources/data-source=ecommDS:read-resource(include-runtime=true,recursive=true)
/subsystem=datasources:read-resource

# Flush datasources
/subsystem=datasources/data-source=ecommDS:flush-idle-connection-in-pool
/subsystem=datasources/data-source=ecommDS:flush-all-connection-in-pool


# HTTP Configuration
/subsystem=undertow/server=default-server/http-listener=default:read-resource(include-runtime=false

# List Subsystems
/:read-children-names(child-type=subsystem)

# How to get interface address
[standalone@localhost:9990 /] cd interface=public
[standalone@localhost:9990 interface=public] :read-resource(include-runtime=true)

# Add a log category
/subsystem=logging/logger=com.your.package.name:add(level=DEBUG)

# Graceful Shutdown [Start / Suspend / Resume
:suspend
:resume
:shutdown()
:shutdown(restart=true)
kill -15 <pid> [Via OS Signal]

# View all system properties
/core-service=platform-mbean/type=runtime:read-attribute(name=system-properties)

# All Operations List 
:read-operation-names  

# Add, read, remove, write- System attribute 
/system-property=foo:add(value=bar)
/system-property=foo:read-resource
/system-property=foo:remove
/system-property=foo:write-attribute(name="value", value="newValue")
