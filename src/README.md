# Spring-Data

## Lernziele
- [ ] Verstehen, was Dependency Injection ist und wie es in Spring verwendet wird.
- [ ] Kennenlernen von Spring Data und dessen Rolle in der Datenbankinteraktion.
- [ ] Die Verwendung von `MongoRepository` zur Interaktion mit einer MongoDB-Datenbank verstehen.
- [ ] Die Bedeutung von Repository-Schnittstellen und deren automatischer Implementierung durch Spring Data verstehen.

## Dependency Injection in Spring
Dependency Injection (DI) ist ein Konzept in Spring, bei dem Abhängigkeiten von einer Klasse nicht selbst erstellt werden, sondern von Spring verwaltet und injiziert werden. Dies ermöglicht eine lose Kopplung und erleichtert das Testen und Erweitern von Anwendungen.

In Spring erfolgt die DI auf verschiedene Arten, wie Konstruktor-Injektion, Setter-Injektion und Feld-Injektion. Hier ist ein einfaches Beispiel für Konstruktor-Injektion:

```java
public class OrderController {
    private final OrderRepository orderRepository;
    
    public OrderController(OrderRepository orderRepository) {
        this.orderRepository = orderRepository;
    }
}
```

In diesem Beispiel wird die `OrderRepository`-Abhängigkeit über den Konstruktor injiziert.


## MongoDB in Spring Boot integrieren

Um eine MongoDB in eine Spring Boot-Anwendung zu integrieren, benötigt ihr die folgenden Schritte:

1. Fügt die MongoDB-Abhängigkeiten zu eurer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-mongodb</artifactId>
</dependency>
```

2. Konfiguriert eure MongoDB-Verbindungs-URL und andere Einstellungen in der `application.properties`-Datei:

```properties
spring.data.mongodb.uri=mongodb+srv://<username>:<password>@<cluster-url>/<database-name>
```

Ersetzt `<username>`, `<password>`, `<cluster-url>` und `<database-name>` durch Ihre MongoDB-Atlas-Daten.

3. Properties als Environment Variable

Wir möchten unsere Passwörter und vertraulichen Daten nicht auf GitHub haben, sondern als Environment Variable. Dazu müssen wir die Properties in der `application.properties` wie folgt anpassen:

```properties
spring.data.mongodb.uri=${MONGODB_URI}
```

4. Setzt die Environment Variable

In IntelliJ könnt ihr die Environment Variable in den Run Configurations setzen. Klickt dazu auf den Run-Button und dann auf "Edit Configurations...".

![1.edit-configurations.png](handout-img%2F1.edit-configurations.png)

Danach geht ihr auf Modify Options und wählt `Environment Variables` aus.

![2.Modify options.png](handout-img%2F2.Modify%20options.png)

Jetzt könnt ihr die Environment Variable setzen.
![3.Environment variables.png](handout-img%2F3.Environment%20variables.png)

![4.Mongo-uri.png](handout-img%2F4.Mongo-uri.png)

5. Erstellt einen Record, der eure Dokumente in der Datenbank repräsentiert:

```java
public record Person (String id, String firstName, String lastName){}
```

6. Einführung in Spring Data

## Verwendung von `MongoRepository`
`MongoRepository` ist eine Spring-Data-Schnittstelle, die die CRUD (Create, Read, Update, Delete)-Operationen für MongoDB-Datenbanken bereitstellt. Hier ist ein einfaches Beispiel, wie Sie es verwenden können:
Der `Person` Record wird in der Datenbank als User Collection gespeichert.
String ist der Datentyp des `Primary Keys`.
```java
public interface PersonRepository extends MongoRepository<Person, String> {
}
```

In diesem Beispiel erstellen wir ein `PersonRepository`, das von `MongoRepository` erbt. Spring Data erstellt automatisch Implementierungen für CRUD-Operationen und Abfragen basierend auf Methodennamen.




## Ressourcen
- [Spring Framework Dokumentation](https://spring.io/projects/spring-framework)
- [Spring Data MongoDB Dokumentation](https://spring.io/projects/spring-data-mongodb)

