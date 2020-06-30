# microservice-s1-day6
Day 6:

Spring Cloud Routing: Zuul

1) Create a project: (cloudserver-netflix-zuul)

2) Add the dependencies in pom.xml:
(Starters - Zuul, Actuator, Web)

<dependency>
<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
<dependency>
<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-starter-web</artifactId>
</dependency>
<dependency>
<groupId>org.springframework.cloud</groupId>
<artifactId>spring-cloud-starter-netflix-zuul</artifactId>
</dependency>

3) Add @EnableZuulProxy annotation

4) Create PreFilter, PostFilter, RouteFilter, ErrorFilter
- extends ZuulFilter

filterType:
- "pre"
- "post"
- "route"
- "error"

5) Register the Filters

------------------------------------

API Gateway - Microservice:

a) storeapp - http://localhost:56757/products

6) In application.properties:

#Zuul routes
zuul.routes.products.url=http://localhost:56757
zuul.routes.products.path=/api/**

#will start the api gateway server @8080
server.port=8080

-------------------------------------

http://localhost:8080/api/products
http://localhost:8080/api/products/1  GET

---------------------------------------------------------------

API Gateway - EurekaRegistry:

a) storeapp - http://product-service/products

1) Create the project:
(cloudserver-netflix-zuul-eureka)

2) In pom.xml:
(Starters - web, actuator, zuul, Eureka Client)

<dependency>
<groupId>org.springframework.cloud</groupId>
<artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>

3) Add @EnableZuulProxy annotation

4) Create PreFilter, PostFilter, RouteFilter, ErrorFilter
- extends ZuulFilter

filterType:
- "pre"
- "post"
- "route"
- "error"

5) Register the Filters

6) In application.properties:

#http://product-service/products

zuul.routes.products.service-id=product-service
zuul.routes.products.path=/api/**

#will start the api gateway server @8080
server.port=8080

#Eureka Server Details
eureka.client.serviceUrl.defaultZone=http://localhost:8761/eureka
eureka.client.register-with-eureka=false

-----------------------------------

http://localhost:8080/api/products
http://localhost:8080/api/products/1  GET

---------------------------------------------------------------


