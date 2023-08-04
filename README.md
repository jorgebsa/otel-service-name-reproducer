# otel-service-name-reproducer

Reproducer to show that the fix for https://github.com/quarkusio/quarkus/issues/33317 does not actually fix all scenarios,
even though unit tests are passing. 

As figured out by @michalvavrik, this happens when the Resource has an empty attribute list. As a workaround, in order
to use the service name on versions 3.2.1 - 3.2.3 one can set a single attribute with any value, and quarkus will resolve
the service name properly.

## Reproducing the error

1) Start the Jaeger all-in-one container with the provided `docker-compose.yml`
2) Start the application with `mvn quarkus:dev`
3) Send a GET request to http://localhost:8080/hello
4) Open Jaeger UI and check the service list, and you will see that the value configured on `quarkus.otel.service.name` was not used
