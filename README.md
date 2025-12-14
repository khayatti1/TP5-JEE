# TP 5.1 – Spring Cloud Zuul API Gateway

## Description

Ce TP met en œuvre une **API Gateway** basée sur **Spring Cloud Netflix Zuul**.
Zuul joue le rôle de **point d’entrée unique** pour les microservices, assure la **découverte des services via Eureka**, le **load balancing** et la **gestion des filtres**.

Le projet s’appuie sur **Spring Cloud Config** et **Eureka Server**.

## Architecture

Le système est composé de :

1. **Config Server**

   * Configuration centralisée
   * Port : 9101

2. **Eureka Server**

   * Registre des microservices
   * Port : 9102

3. **Zuul Server (API Gateway)**

   * Routage et filtrage des requêtes
   * Enregistré auprès d’Eureka
   * Port : 9004

4. **Microservice Produits**

   * Client Eureka
   * Plusieurs instances
   * Ports : 9001, 9011

## Fonctionnalités

* Mise en place d’une API Gateway Zuul
* Enregistrement de Zuul auprès d’Eureka
* Routage dynamique vers les microservices
* Load balancing automatique (Round-Robin)
* Accès aux services via une URL unique
* Mise en œuvre de filtres Zuul (pre / post)

## Annotations clés

* `@EnableZuulProxy` : activation de l’API Gateway
* `@EnableDiscoveryClient` : enregistrement dans Eureka
* `ZuulFilter` : interception et traitement des requêtes

## Accès aux services

* Eureka Server :

  ```
  http://localhost:9102/
  ```
* Accès direct au microservice :

  ```
  http://localhost:9001/Produits
  ```
* Accès via Zuul Gateway :

  ```
  http://localhost:9004/microservice-produits/Produits
  ```

## Exécution

### Démarrer les services

```bash
# Config Server
cd config-server
mvn spring-boot:run

# Eureka Server
cd eurekaserver
mvn spring-boot:run

# Zuul Server
cd zuul-server
mvn spring-boot:run
```

### Démarrer les instances du microservice Produits

```bash
mvn spring-boot:run -Dserver.port=9001
mvn spring-boot:run -Dserver.port=9011
```

## Vérifications

* Vérifier l’enregistrement des services dans Eureka
* Accéder aux produits via Zuul
* Observer la répartition de charge entre les instances
* Vérifier l’exécution des filtres Zuul dans la console

## Objectifs pédagogiques

* Comprendre le rôle d’une API Gateway
* Mettre en place le routage dynamique
* Découvrir le load balancing côté client
* Implémenter des filtres de pré et post-traitement
* Centraliser l’accès aux microservices

---

**MOHAMMED EL KHAYATI & MOUAD MOUDID--5IIR11**
