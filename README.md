# Hello Spring with s2i

Simple Spring Boot app to demo OpenShift source-to-image.

## Endpoints:

* "/"  
says hello
* "/actuator/health/readiness"  
readiness probe
* "/actuator/health/liveness"  
liveness probe

## Build with s2i

`oc new-app openshift/java:openjdk-17-ubi8~https://github.com/nikolaus-lemberski/hello-spring-s2i`

## Make public

`oc expose svc hello-spring-s2i`

`oc get route`

## Add healthchecks

```bash
oc set probe deployment hello-fastapi --readiness --get-url=http://:8080/actuator/health/readiness --initial-delay-seconds=10 --period=5
oc set probe deployment hello-fastapi --liveness --get-url=http://:8080/actuator/health/liveness --initial-delay-seconds=10 --period=5```