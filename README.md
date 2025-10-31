# Proyecto – Spring Boot + Thymeleaf (CRUD de Tutoriales)
## 1) URL de la página

`http://68.155.147.140:8080/tutorials` 


## 2) Descripción del proyecto
Aplicación web **CRUD** para gestionar **Tutoriales**, construida con **Spring Boot** (Web/MVC), **Thymeleaf** para vistas, y **Spring Data JPA** sobre **PostgreSQL** (configurado vía variables de entorno).
Permite **crear, listar (con búsqueda)**, **editar**, **eliminar** y **cambiar el estado de publicación** de un tutorial.

**Tecnologías principales**
- Spring Boot (Web / MVC)
- Thymeleaf (motor de plantillas)
- Spring Data JPA (Hibernate) con PostgreSQL
- Maven (Spring Boot Maven Plugin)


## 3) Estructura del proyecto (real)

```
src/
├─ main/
│  ├─ java/com/bezkoder/spring/thymeleaf/
│  │  ├─ controller/
│  │  │  └─ TutorialController.java
│  │  ├─ entity/
│  │  │  └─ Tutorial.java
│  │  ├─ repository/
│  │  │  └─ TutorialRepository.java
│  │  └─ SpringBootThymeleafExampleApplication.java
│  └─ resources/
│     ├─ templates/                 # Vistas Thymeleaf (.html)
│     ├─ static/                    # Recursos estáticos (CSS/JS/img)
│     └─ application.properties     # Configuración
└─ test/
```

## 4) Explicación de carpetas

- **controller/**: Controladores Spring MVC. Aquí está `TutorialController` con la lógica de rutas y bindings a vistas Thymeleaf.
- **entity/**: Entidades **JPA**; `Tutorial` mapea la tabla `tutorials` con campos `id`, `title`, `description`, `level`, `published`.
- **repository/**: Repositorios **Spring Data JPA**. `TutorialRepository` extiende `JpaRepository<Tutorial, Integer>` e incluye query derivada `findByTitleContainingIgnoreCase` y un `@Query` de actualización para `published`.
- **resources/**: Plantillas Thymeleaf (`templates`), recursos estáticos y `application.properties` con la configuración de la app.


## 5) Configuración y entorno
El proyecto está listo para **PostgreSQL** usando **variables de entorno**. Ejemplo de `application.properties`:

```properties
spring.h2.console.enabled=false
spring.h2.console.path=/h2-ui

spring.datasource.url=${SPRING_DATASOURCE_URL}
spring.datasource.username=${SPRING_DATASOURCE_USERNAME}
spring.datasource.password=${SPRING_DATASOURCE_PASSWORD}
spring.datasource.driver-class-name=org.postgresql.Driver
 
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
spring.jpa.hibernate.ddl-auto= update
```


## 6) Cómo ejecutar el proyecto

### Desarrollo

1. Exportar variables de entorno para PostgreSQL:
   ```bash
   export SPRING_DATASOURCE_URL=jdbc:postgresql://localhost:5432/tutorialsdb
   export SPRING_DATASOURCE_USERNAME=postgres
   export SPRING_DATASOURCE_PASSWORD=postgres
   ```
2. Ejecutar la aplicación:
   ```bash
   mvn spring-boot:run
   ```
3. Abrir en el navegador: `http://68.155.147.140:8080/tutorials` 


## 7) Endpoints o peticiones disponibles (rutas reales)

| Funcionalidad | Ruta | Método | Descripción |
|---|---|---|---|
| Listar tutoriales (con búsqueda opcional) | `/tutorials` | GET | Lista todos los tutoriales o filtra por título (contiene, ignore case). |
| Formulario de creación | `/tutorials/new` | GET | Muestra el formulario para crear un tutorial. |
| Editar por ID | `/tutorials/{id}` | GET | Carga un tutorial por ID y muestra el formulario de edición. |
| Eliminar por ID | `/tutorials/delete/{id}` | GET | Elimina un tutorial por ID y redirige a /tutorials. |




## 8) Arquitectura del proyecto

![alt text](image-1.png)


