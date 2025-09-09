# 🌱 Spring Annotations Guide

A **comprehensive reference and cheatsheet** for commonly used Spring and Spring Boot annotations. Includes **detailed explanations, use cases, and examples** for quick learning and practical implementation.

---

## 📑 Quick Reference Table

| Annotation        | Purpose                                          |
| ----------------- | ------------------------------------------------ |
| `@Autowired`      | Injects dependencies automatically               |
| `@Profile`        | Activates beans based on environment profile     |
| `@Component`      | Generic component scan target                    |
| `@Service`        | Business logic layer component                   |
| `@Repository`     | Data access component with exception translation |
| `@Controller`     | Web layer component (non-REST)                   |
| `@RestController` | Combines `@Controller` + `@ResponseBody`         |
| `@Configuration`  | Bean definition source                           |
| `@Bean`           | Declares a bean managed by Spring                |
| `@Qualifier`      | Disambiguates multiple beans of same type        |
| `@Value`          | Injects values from properties/environment       |

---

## 🌿 Core Spring Annotations

### `@Bean`

* **Purpose**: Declares a method that produces a bean managed by the Spring IoC container.
* **Example:**

```java
@Configuration
public class AppConfig {
    @Bean
    public Dog dog() {
        return new Dog("Tommy");
    }
}
```

### Stereotype Annotations

* **`@Component`** – Generic Spring-managed component.
* **`@Service`** – Marks business logic layer beans.
* **`@Repository`** – DAO layer bean, auto-translates exceptions.
* **`@Controller`** – MVC controller for handling HTTP requests.
* **`@RestController`** – `@Controller` + `@ResponseBody`, returns JSON/XML directly.

**Example:**

```java
@Service
public class CarService {
    public String getCarName() {
        return "Tesla Model 3";
    }
}

@RestController
public class CarController {
    @Autowired
    private CarService carService;

    @GetMapping("/car")
    public String car() {
        return carService.getCarName();
    }
}
```

### `@Configuration`

* Marks a class as a configuration class, defining beans.
* Often used with `@Bean`.

---

## 🔄 Bean Lifecycle Annotations

### `@PostConstruct`

Executed after dependency injection, for initialization.

```java
@Component
public class InitExample {
    @PostConstruct
    public void init() {
        System.out.println("Bean initialized!");
    }
}
```

### `@PreDestroy`

Executed before bean destruction, often for cleanup.

```java
@Component
public class DestroyExample {
    @PreDestroy
    public void cleanup() {
        System.out.println("Bean destroyed!");
    }
}
```

---

## ⚙️ Configuration Annotations

* **`@Import`** – Import another config class.
* **`@PropertySource`** – Load properties from file.
* **`@Value`** – Inject values from properties/env.
* **`@ComponentScan`** – Configure package scanning.

**Example:**

```java
@Configuration
@PropertySource("classpath:application.properties")
public class AppConfig {

    @Value("${app.name}")
    private String appName;

    @Bean
    public String printAppName() {
        return appName;
    }
}
```

---

## 🏷️ Bean Properties

* `@Lazy` – Lazy initialization.
* `@Profile` – Activate beans per environment.
* `@Scope` – Define bean scope (singleton, prototype).
* `@DependsOn` – Create dependency order.
* `@Order` – Sorting order of beans.
* `@Primary` – Preferred bean if multiple candidates.
* `@Conditional` – Create beans conditionally.

---

## 💉 Bean Injection

### `@Autowired`

Injects dependencies.

```java
@Component
public class Car {
    @Autowired
    private Engine engine;
}
```

### `@Qualifier`

Disambiguates multiple beans.

```java
@Component("petrolEngine")
class PetrolEngine implements Engine {}

@Component("dieselEngine")
class DieselEngine implements Engine {}

@Component
class Car {
    @Autowired
    @Qualifier("dieselEngine")
    private Engine engine;
}
```

---

## ✅ Validation

* `@Valid` – Apply validation rules.
* `@NotNull`, `@NotEmpty`, `@NotBlank` – Field constraints.
* `@Past`, `@Future` – Date/time constraints.

**Example:**

```java
@PostMapping("/addUser")
public ResponseEntity<String> addUser(@Valid @RequestBody User user) {
    return ResponseEntity.ok("User added");
}
```

---

## 🚀 Spring Boot Annotations

* **`@SpringBootApplication`** – Combines `@Configuration`, `@EnableAutoConfiguration`, `@ComponentScan`.
* **`@EnableAutoConfiguration`** – Enables Spring Boot’s auto-configuration.
* **`@ConfigurationProperties`** – Binds external properties.

**Example:**

```java
@SpringBootApplication
public class MyApp {
    public static void main(String[] args) {
        SpringApplication.run(MyApp.class, args);
    }
}
```

---

## 🧪 Spring Boot Testing

* `@SpringBootTest` – Full application context.
* `@WebMvcTest` – Web layer only.
* `@DataJpaTest` – JPA components.
* `@MockBean` – Mock bean.

**Example:**

```java
@SpringBootTest
class CarServiceTest {
    @Autowired
    private CarService carService;

    @Test
    void testCarName() {
        assertEquals("Tesla Model 3", carService.getCarName());
    }
}
```

---

## 🗄️ Spring JPA and Hibernate

* `@Entity`, `@Table`, `@Id`, `@GeneratedValue` – Entity mapping.
* `@ManyToOne`, `@OneToOne`, `@ManyToMany`, `@JoinColumn`, `@JoinTable` – Relationships.
* `@CreationTimestamp`, `@UpdateTimestamp` – Auto timestamps.

**Example:**

```java
@Entity
@Table(name="users")
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @OneToMany(mappedBy = "user")
    private List<Order> orders;
}
```

---

## 🔐 Spring Security

* `@EnableWebSecurity` – Enable Spring Security.
* `@PreAuthorize`, `@PostAuthorize` – Method-level security.
* `@Secured`, `@RolesAllowed` – Role-based access.

**Example:**

```java
@RestController
public class AdminController {

    @PreAuthorize("hasRole('ADMIN')")
    @GetMapping("/admin")
    public String adminOnly() {
        return "Admin content";
    }
}
```

---

## 🎭 Spring AOP (Aspect-Oriented Programming)

* `@Aspect` – Define aspect class.
* `@Before`, `@After`, `@Around` – Define advices.
* `@EnableAspectJAutoProxy` – Enable proxy-based AOP.

**Example:**

```java
@Aspect
@Component
public class LoggingAspect {

    @Before("execution(* com.example.service.*.*(..))")
    public void logBefore(JoinPoint joinPoint) {
        System.out.println("Method called: " + joinPoint.getSignature());
    }
}
```

---

## 📚 Additional References

* [Spring Framework Documentation](https://docs.spring.io/spring-framework/docs/current/reference/html/)
* [Baeldung Spring Tutorials](https://www.baeldung.com/)
* *Spring in Action* (Book)

---

🚀 This guide now covers **all major annotations** with **detailed explanations + code examples** for real-world usage.
