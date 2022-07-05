
Application full stack: REACTJS + REDUX + JAVA + SPRINGBOOT + POSTGRES/H2
===========================================================================

* Java 17
* Docker
* Maven
* NodeJS
* PostgresSQL
* H2
* ReactJS
* SpringBoot

# Lancement H2 en locale


Génerer une base de donnée H2 en locale puis lancer le backend:

```
> mvn clean install -PdropDb,updateDb
> mvn spring-boot:run -Dspring-boot.run.jvmArguments="-Dspring.devtools.restart.enabled=false" -Dspring-boot.run.arguments=--env=local-h2
```

Génerer le frontend puis lancer l'IHM

```
> mvn install -Pinstall-reactui,npm-install
> cd frontworking
> npm start
```

Puis acceder à l'application via l'url: http://localhost:8080/testproject

# Run avec Docker + postgres

Après avoir fait un build du projet comme indiqué ci dessus, une base données h2 a été générée à l'emplacement: target/localDb/testproject.
Cette base de données est copié dans l'image docker pendant le build du snapshot.

```
> docker run --name testproject -p 8080:8080 -e JAVA_TOOL_OPTIONS="-Denv=local-h2" neocloud4j/testproject:1.0-SNAPSHOT 
```


```
> docker network create test_network
> docker run -d --name postgres --network test_network -p 5432:5432 -e POSTGRES_PASSWORD=postgres -e POSTGRES_USER=postgres postgres
> mvn clean install -PdropDb,updateDb -Denv=local-postgres
> mvn spring-boot:run -Dspring-boot.run.jvmArguments="-Dspring.devtools.restart.enabled=false" -Dspring-boot.run.arguments=--env=local-postgres
```

Run
```
> docker run --name testproject -p 8080:8080 -e JAVA_TOOL_OPTIONS="-Denv=local-postgres" neocloud4j/testproject:1.0-SNAPSHOT 
```

Puis acceder à l'application via l'url: http://localhost:8080/testproject


# Feedback

Contact: support@nexitia.com
