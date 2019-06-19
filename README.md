# Nacos/Spring Cloud Config validation project

## Environment
There are two application:

1. **Client application**, with nacos-discovery-starter and spring-cloud-config-client
2. **Spring Cloud Config Server**, with spring-cloud-config-server

## Goal
Config server URL will looked up via discovery

## Reproduce
1. Run config-server, and register in nacos named `configserver`
2. Run client, with nacos discovery and config-client. (application run failed)

* If put configuration of discovery and config in application.yml, client would be up, but could not get right config-server URL
* If put this configuration in bootstrap.yml, application could not run.


## Problem
Errors occur

```
org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'discoveryClientConfigServiceBootstrapConfiguration': Unsatisfied dependency expressed through field 'instanceProvider'; nested exception is org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'configServerInstanceProvider' defined in org.springframework.cloud.config.client.DiscoveryClientConfigServiceBootstrapConfiguration: Unsatisfied dependency expressed through method 'configServerInstanceProvider' parameter 0; nested exception is org.springframework.beans.factory.NoSuchBeanDefinitionException: No qualifying bean of type 'org.springframework.cloud.client.discovery.DiscoveryClient' available: expected at least 1 bean which qualifies as autowire candidate. Dependency annotations: {}
```