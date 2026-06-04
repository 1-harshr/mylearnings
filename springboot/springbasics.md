
## Core Spring Annotations

| Annotation               | Purpose                                                                                                    |
| ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| `@SpringBootApplication` | Main application entry point. Combines `@Configuration`, `@EnableAutoConfiguration`, and `@ComponentScan`. |
| `@Configuration`         | Declares a configuration class.                                                                            |
| `@Bean`                  | Creates a Spring-managed bean.                                                                             |
| `@Component`             | Generic Spring-managed component.                                                                          |
| `@Service`               | Service/business logic layer bean.                                                                         |
| `@Repository`            | DAO/repository bean. Enables exception translation.                                                        |
| `@Controller`            | MVC controller returning views.                                                                            |
| `@RestController`        | REST API controller (`@Controller + @ResponseBody`).                                                       |
| `@ComponentScan`         | Specifies packages to scan for beans.                                                                      |
| `@Scope`                 | Defines bean scope (`singleton`, `prototype`, etc.).                                                       |
| `@Lazy`                  | Delays bean creation until first use.                                                                      |

---

## Dependency Injection

|Annotation|Purpose|
|---|---|
|`@Autowired`|Inject dependency automatically.|
|`@Qualifier`|Specify which bean to inject.|
|`@Primary`|Default bean when multiple candidates exist.|
|`@Value`|Inject property value.|
|`@Resource`|JSR-250 dependency injection.|
|`@Inject`|JSR-330 dependency injection.|

Example:

```java
@Service
public class UserService {

    @Autowired
    @Qualifier("mysqlRepo")
    private UserRepository repo;
}
```

---

## REST API

|Annotation|Purpose|
|---|---|
|`@RequestMapping`|Base mapping.|
|`@GetMapping`|HTTP GET endpoint.|
|`@PostMapping`|HTTP POST endpoint.|
|`@PutMapping`|HTTP PUT endpoint.|
|`@DeleteMapping`|HTTP DELETE endpoint.|
|`@PatchMapping`|HTTP PATCH endpoint.|
|`@RequestParam`|Query parameter.|
|`@PathVariable`|URL path variable.|
|`@RequestBody`|Request payload.|
|`@ResponseBody`|Return object as JSON/XML.|
|`@ResponseStatus`|Custom HTTP status.|
|`@RequestHeader`|Read HTTP header.|
|`@CookieValue`|Read cookie value.|
|`@CrossOrigin`|Enable CORS.|

Example:

```java
@GetMapping("/users/{id}")
public User getUser(
        @PathVariable Long id,
        @RequestParam(required = false) String role) {
    return service.getUser(id);
}
```

---

## Validation

|Annotation|Purpose|
|---|---|
|`@Valid`|Trigger validation.|
|`@Validated`|Validation at class/method level.|
|`@NotNull`|Must not be null.|
|`@NotEmpty`|Collection/string not empty.|
|`@NotBlank`|String not blank.|
|`@Size`|Length/size constraint.|
|`@Min`|Minimum value.|
|`@Max`|Maximum value.|
|`@Positive`|Positive number.|
|`@Negative`|Negative number.|
|`@Email`|Valid email.|
|`@Pattern`|Regex validation.|
|`@Past`|Date must be in past.|
|`@Future`|Date must be in future.|

Example:

```java
public class UserDto {

    @NotBlank
    private String name;

    @Email
    private String email;
}
```

---

## Exception Handling

|Annotation|Purpose|
|---|---|
|`@ExceptionHandler`|Handle specific exception.|
|`@ControllerAdvice`|Global MVC exception handling.|
|`@RestControllerAdvice`|Global REST exception handling.|

Example:

```java
@RestControllerAdvice
public class GlobalHandler {

    @ExceptionHandler(Exception.class)
    public String handle(Exception ex) {
        return ex.getMessage();
    }
}
```

---

## JPA / Hibernate

|Annotation|Purpose|
|---|---|
|`@Entity`|JPA entity.|
|`@Table`|Table mapping.|
|`@Id`|Primary key.|
|`@GeneratedValue`|Auto-generate ID.|
|`@Column`|Column mapping.|
|`@Transient`|Not persisted.|
|`@Enumerated`|Enum mapping.|
|`@Lob`|Large object (BLOB/CLOB).|
|`@Version`|Optimistic locking.|

### Relationships

|Annotation|Purpose|
|---|---|
|`@OneToOne`|One-to-one relation.|
|`@OneToMany`|One-to-many relation.|
|`@ManyToOne`|Many-to-one relation.|
|`@ManyToMany`|Many-to-many relation.|
|`@JoinColumn`|Foreign key column.|
|`@JoinTable`|Join table definition.|

Example:

```java
@Entity
public class Order {

    @Id
    @GeneratedValue
    private Long id;

    @ManyToOne
    @JoinColumn(name = "user_id")
    private User user;
}
```

---

## Spring Data JPA

|Annotation|Purpose|
|---|---|
|`@EnableJpaRepositories`|Enable repository scanning.|
|`@Query`|Custom JPQL/SQL query.|
|`@Modifying`|Update/delete query.|
|`@Param`|Named query parameter.|

Example:

```java
@Query("SELECT u FROM User u WHERE u.email = :email")
User findByEmail(@Param("email") String email);
```

---

## Transactions

|Annotation|Purpose|
|---|---|
|`@Transactional`|Transaction management.|

Example:

```java
@Transactional
public void transferMoney() {
    ...
}
```

---

## Configuration Properties

|Annotation|Purpose|
|---|---|
|`@ConfigurationProperties`|Bind properties to POJO.|
|`@EnableConfigurationProperties`|Enable property binding.|
|`@PropertySource`|Load custom property file.|

Example:

```java
@ConfigurationProperties(prefix = "app")
public class AppConfig {
    private String name;
}
```

---

## Security

|Annotation|Purpose|
|---|---|
|`@EnableWebSecurity`|Enable Spring Security.|
|`@EnableMethodSecurity`|Enable method security.|
|`@PreAuthorize`|Method-level authorization.|
|`@PostAuthorize`|Post-execution authorization.|
|`@RolesAllowed`|Restrict by role.|
|`@Secured`|Role-based access control.|

Example:

```java
@PreAuthorize("hasRole('ADMIN')")
public void deleteUser() {
}
```

---

## Scheduling & Async

|Annotation|Purpose|
|---|---|
|`@EnableScheduling`|Enable scheduler.|
|`@Scheduled`|Run task periodically.|
|`@EnableAsync`|Enable async execution.|
|`@Async`|Execute method asynchronously.|

Example:

```java
@Scheduled(cron = "0 0 * * * *")
public void runEveryHour() {
}
```

---

## Testing

|Annotation|Purpose|
|---|---|
|`@SpringBootTest`|Full application context test.|
|`@WebMvcTest`|Controller test.|
|`@DataJpaTest`|Repository test.|
|`@MockBean`|Mock Spring bean.|
|`@TestConfiguration`|Test-specific configuration.|

---

## Lombok (Very Common with Spring Boot)

|Annotation|Purpose|
|---|---|
|`@Getter`|Generate getters.|
|`@Setter`|Generate setters.|
|`@Data`|Getter + Setter + Equals + HashCode + ToString.|
|`@Builder`|Builder pattern.|
|`@NoArgsConstructor`|No-arg constructor.|
|`@AllArgsConstructor`|All-args constructor.|
|`@RequiredArgsConstructor`|Constructor for final fields.|
|`@Slf4j`|Logger generation.|

---

## Most Frequently Used in Real Projects

```java
@SpringBootApplication

@RestController
@RequestMapping
@GetMapping
@PostMapping
@RequestBody
@PathVariable
@RequestParam

@Service
@Repository
@Component

@Autowired
@RequiredArgsConstructor

@Entity
@Id
@GeneratedValue
@Column
@OneToMany
@ManyToOne

@Transactional

@Valid
@NotNull
@NotBlank

@ExceptionHandler
@RestControllerAdvice

@ConfigurationProperties

@PreAuthorize

@Scheduled
@Async
```

These ~35 annotations cover roughly 90% of what you'll encounter in typical Spring Boot backend development.
