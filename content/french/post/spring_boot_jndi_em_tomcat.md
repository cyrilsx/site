---
title: "Spring boot - Configuration d'une datasource avec jndi et tomcat"
date: 2023-07-02T21:05:05-05:00
tags: [dev, java] 
---
# Spring boot - Comment déclarer une source de données JNDI

Dans certaine situation, nous devons intégrer des dépendances qui ont besoin d'une source de données _(datasource)_ JNDI ce qui peut être problématique lors de 
son intégration dans une application spring-boot avec le serveut tomcat embarqué.

Heureusement, il est possible d'initialiser le datasource comme ci-dessous :

```java
@SpringBootApplication 
public class ApplicationConfigMain {

 public static void main(String[] args) {
   SpringApplication.run(ApplicationConfigMain.class, args);
 }

 @Bean
 public TomcatServletWebServerFactory tomcatFactory(DataSourceProperties dataSource) {
   return new TomcatServletWebServerFactory() {
     @Override
     protected TomcatWebServer getTomcatWebServer(org.apache.catalina.startup.Tomcat tomcat) {
       tomcat.enableNaming();
       return super.getTomcatWebServer(tomcat);
     }

     @Override
     protected void postProcessContext(Context context) {
       ContextResource resource = new ContextResource();
       resource.setName("jdbc/myDS");
       resource.setType(DataSource.class.getName());
       resource.setProperty("driverClassName", "org.postgresql.Driver");
       resource.setProperty("url", dataSource.getUrl());
       resource.setProperty("username", dataSource.getUsername());
       resource.setProperty("password", dataSource.getPassword());
       context.getNamingResources().addResource(resource);
     }
   };
  }
}
```
