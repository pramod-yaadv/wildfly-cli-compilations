## Wildfly-cli-compilations (standalone mode)
This repository comprises of commonly used Wildfly cli commands in standalone to perform or manage Wildfly in Runtime. Currently release only for standalone mode and later will update on domain mode.

## Index
- [Enable Datasource Stats](https://github.com/pramod-yaadv/wildfly-cli-compilations/blob/main/README.md#enable-datasource-stats)
- [See statistics](https://github.com/pramod-yaadv/wildfly-cli-compilations/blob/main/README.md#see-statistics)
- [List all available datasources](https://github.com/pramod-yaadv/wildfly-cli-compilations/blob/main/README.md#list-all-available-datasources)
- [Write, remove attributes](https://github.com/pramod-yaadv/wildfly-cli-compilations/blob/main/README.md#write-remove-attributes)
- [DataSource](https://github.com/pramod-yaadv/wildfly-cli-compilations/blob/main/README.md#datasource)
- [Flush datasources](https://github.com/pramod-yaadv/wildfly-cli-compilations/blob/main/README.md#flush-datasources)
- [HTTP Configuration](https://github.com/pramod-yaadv/wildfly-cli-compilations/blob/main/README.md#http-configuration)
- [List Subsystems](https://github.com/pramod-yaadv/wildfly-cli-compilations/blob/main/README.md#list-subsystems)
- [To get interface address](https://github.com/pramod-yaadv/wildfly-cli-compilations/blob/main/README.md#how-to-get-interface-address)
- [Add a log category](https://github.com/pramod-yaadv/wildfly-cli-compilations/blob/main/README.md#add-a-log-category)
- [Graceful Shutdown - Start / Shutdown/ Suspend / Resume](https://github.com/pramod-yaadv/wildfly-cli-compilations/blob/main/README.md#graceful-shutdown-start--suspend--resume)
- [View all system properties](https://github.com/pramod-yaadv/wildfly-cli-compilations/blob/main/README.md#view-all-system-properties)
- [All Operations List](https://github.com/pramod-yaadv/wildfly-cli-compilations/blob/main/README.md#all-operations-list)
- [Add, read, remove, write- System attribute](https://github.com/pramod-yaadv/wildfly-cli-compilations/blob/main/README.md#add-read-remove-write--system-attribute)

******

### Enable Datasource Stats 
/subsystem=datasources/data-source=ecommDS/statistics=pool:write-attribute(name=statistics-enabled,value=true)
/subsystem=datasources/data-source=ecommDS/statistics=jdbc:write-attribute(name=statistics-enabled,value=true)
/subsystem=datasources/data-source=ecommDS:write-attribute(name=statistics-enabled,value=true)

---

### See statistics
/subsystem=datasources/data-source=ecommDS/statistics=pool:read-resource(include-runtime=true)
/subsystem=datasources/data-source=ecommDS/statistics=jdbc:read-resource(include-runtime=true)
/subsystem=datasources/data-source=ecommDS:read-resource(include-runtime=true,recursive=true)

---

### List all available datasources
/subsystem=datasources:read-resource

---

### Write, remove attributes
/subsystem=datasources/data-source=ecommDS:write-attribute(name=query-timeout,value=300)
/subsystem=datasources/data-source=ecommDS:undefine-attribute(name=query-timeout)

---

### DataSource
/subsystem=datasources/data-source=ecommDS:test-connection-in-pool()
/subsystem=datasources/data-source=ecommDS/statistics=pool:read-resource(include-runtime=true)
/subsystem=datasources/data-source=ecommDS/statistics=jdbc:read-resource(include-runtime=true)
/subsystem=datasources/data-source=ecommDS:read-resource(include-runtime=true,recursive=true)
/subsystem=datasources:read-resource

---

### Flush datasources
/subsystem=datasources/data-source=ecommDS:flush-idle-connection-in-pool
/subsystem=datasources/data-source=ecommDS:flush-all-connection-in-pool

---

### HTTP Configuration
/subsystem=undertow/server=default-server/http-listener=default:read-resource(include-runtime=false

---

### List Subsystems
/:read-children-names(child-type=subsystem)

---

### How to get interface address
[standalone@localhost:9990 /] cd interface=public
[standalone@localhost:9990 interface=public] :read-resource(include-runtime=true)

---

### Add a log category
/subsystem=logging/logger=com.your.package.name:add(level=DEBUG)

---

### Graceful Shutdown [Start / Suspend / Resume
:suspend
:resume
:shutdown()
:shutdown(restart=true)
kill -15 <pid> [Via OS Signal]

---

### View all system properties
/core-service=platform-mbean/type=runtime:read-attribute(name=system-properties)

---

### All Operations List 
:read-operation-names  

---

### Add, read, remove, write- System attribute 
/system-property=foo:add(value=bar)
/system-property=foo:read-resource
/system-property=foo:remove
/system-property=foo:write-attribute(name="value", value="newValue")
