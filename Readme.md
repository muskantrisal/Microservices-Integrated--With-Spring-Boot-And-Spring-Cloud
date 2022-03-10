# Microservices with Spring Boot and Spring Cloud


Contents:-

- Established Communication between Microservices
- Centralized Microservice Configuration with Spring Cloud Config Server
- Used Spring Cloud Bus to exchange messages about Configuration updates
- Simplified communication with other Microservices using Feign REST Client
- Implemented client side load balancing with Ribbon
- Implemented dynamic scaling using Eureka Naming Server and Ribbon
- Implemented API Gateway with Zuul
- Implemented Distributed tracing with Spring Cloud Sleuth and Zipkin
- Implemented Fault Tolerance with Zipkin

## Microservices Step by Step

#### Spring Cloud Config Server
- Step 00 - 04 - Limits Microservice and Spring Cloud Config Server
- Step 01 - Set up Limits Microservice
- Step 02 - Created a hard coded limits service
- Step 03 - Enhanced limits service to pick up configuration from application properties
- Step 04 - Set up Spring Cloud Config Server
- Step 05 - Installed Git
- Step 06 - Created Local Git Repository
- Step 07 - Connected Spring Cloud Config Server to Local Git Repository
- Step 08 - Configured for Multiple Environments in Git Repository
- Step 09 - Connected Limits Service to Spring Cloud Config Server
- Step 10 - Configured Profiles for Limits Service
- Step 11 - Reviewed Spring Cloud Config Server

#### Implementing 2 Microservices with Eureka Naming Server, Ribbon and Feign
- Step 12 - Currency Conversion and Currency Exchange Microservices
- Step 13 - Set up Currency Exchange Microservice
- Step 14 - Created a simple hard coded currency exchange service
- Step 15 - Set up Dynamic Port in the the Response
- Step 16 - Configured JPA and Initialized Data
- Step 17 - Created a JPA Repository
- Step 18 - Set up Currency Conversion Microservice
- Step 19 - Created a service for currency conversion
- Step 20 - Invoked Currency Exchange Microservice from Currency Conversion Microservice
- Step 21 - Used Feign REST Client for Service Invocation
- Step 22 - Set up client side load balancing with Ribbon
- Step 23 - Ran client side load balancing with Ribbon
- Step 24 - Naming Server
- Step 25 - Set up Eureka Naming Server
- Step 26 - Connected Currency Conversion Microservice to Eureka
- Step 27 - Connected Currency Exchange Microservice to Eureka
- Step 28 - Distributed calls using Eureka and Ribbon
- Step 29 - Implemented Eureka, Ribbon and Feign

#### API Gateways and Distributed Tracing
- Step 30 - API Gateways
- Step 31 - Set up Zuul API Gateway
- Step 32 - Implemented Zuul Logging Filter
- Step 33 - Executed a request through Zuul API Gateway
- Step 34 - Set up Zuul API Gateway between microservice invocations
- Step 35 - Distributed Tracing
- Step 36 - Implemented Spring Cloud Sleuth
- Step 37 - Distributed Tracing with Zipkin
- Step 38 - Installed Rabbit MQ
- Step 39 - Set up Distributed Tracing with Zipkin
- Step 40 - Connected microservices to Zipkin
- Step 41 - Used Zipkin UI Dashboard to trace requests

#### Spring Cloud Bus and Hysterix
- Step 42 - Spring Cloud Bus
- Step 43 - Implemented Spring Cloud Bus
- Step 44 - Fault Tolerance with Hystrix


## Ports

|     Application       |     Port          |
| ------------- | ------------- |
| Limits Service | 8080, 8081, ... |
| Spring Cloud Config Server | 8888 |
|  |  |
| Currency Exchange Service | 8000, 8001, 8002, ..  |
| Currency Conversion Service | 8100, 8101, 8102, ... |
| Netflix Eureka Naming Server | 8761 |
| Netflix Zuul API Gateway Server | 8765 |
| Zipkin Distributed Tracing Server | 9411 |


## URLs

|     Application       |     URL          |
| ------------- | ------------- |
| Limits Service | http://localhost:8080/limits http://localhost:8080/actuator/refresh  (POST)|
|Spring Cloud Config Server| http://localhost:8888/limits-service/default http://localhost:8888/limits-service/dev |
|  Currency Converter Service - Direct Call| http://localhost:8100/currency-converter/from/USD/to/INR/quantity/10|
|  Currency Converter Service - Feign| http://localhost:8100/currency-converter-feign/from/EUR/to/INR/quantity/10000|
| Currency Exchange Service | http://localhost:8000/currency-exchange/from/EUR/to/INR http://localhost:8001/currency-exchange/from/USD/to/INR|
| Eureka | http://localhost:8761/|
| Zuul - Currency Exchange & Exchange Services | http://localhost:8765/currency-exchange-service/currency-exchange/from/EUR/to/INR http://localhost:8765/currency-conversion-service/currency-converter-feign/from/USD/to/INR/quantity/10|
| Zipkin | http://localhost:9411/zipkin/ |
| Spring Cloud Bus Refresh | http://localhost:8080/actuator/bus-refresh (POST)|


## Some more Instructions

```
POST localhost:8080/actuator/refresh
POST localhost:8080/actuator/bus-refresh

Run this project only in intellij

1. Install erlang and rabbit mq in your system
2. Download zipkin server jar and keep it in the same folder



3. While rabbitmq service is running in BG

set RABBIT_URI=amqp://localhost                        
java -jar zipkin-server-2.12.9-exec.jar   (To launch Zipkin server)


NOTE:- If it's the 1st time you're setting up your project make sure to initialise  git-localconfig-repo as a git repo so that spring-cloud-config-server could pick up the changes, and change the gitrepo path in application.properties file of spring-cloud-config-server.
```

## Zipkin Installation

Quick Start Page
- https://zipkin.io/pages/quickstart

Downloading Zipkin Jar(After downloading place this jar in same directory as your project)
- https://search.maven.org/remote_content?g=io.zipkin.java&a=zipkin-server&v=LATEST&c=exec

Command to run
```
set RABBIT_URI=amqp://localhost                        
java -jar zipkin-server-2.12.9-exec.jar (here give the name of the jar)
```

## VM Argument (To run the application with different port)

-Dserver.port=8001

##In short when you setup the application for the 1st time you have to:-(To be performed only in intelliJ)

- Install erlang and RabbitMQ for windows
- Download and place zipkin-server-2.12.9-exec.jar in your main directory
- Update the gitrepo path in application.properties file of spring-cloud-config-server
- Initialise an empty git repository in git-localconfig-repo
- In the base folder run :-
  - set RABBIT_URI=amqp://localhost
  - java -jar zipkin-server-2.12.9-exec.jar
- Then start all your services in the following order
  - netflix-eureka-naming-server
  - netflix-zuul-api-gateway-server
  - currency-exchange-service
  - currency-conversion-service
  - spring-cloud-config-server
  - limits-service
