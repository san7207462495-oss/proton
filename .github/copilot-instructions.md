# AI Coding Agent Instructions for vProfile Project

## Project Overview
This is a Spring MVC web application (vProfile) built as a WAR file for Tomcat deployment. It uses XML-based Spring configuration and integrates with external services (MySQL, Memcached, RabbitMQ, Elasticsearch) running on separate hosts.

## Architecture
- **Frontend**: JSP views under `/WEB-INF/views/`
- **Backend**: Spring MVC controllers, services, repositories
- **Data**: JPA entities with Jakarta Persistence
- **Config**: XML files in `WEB-INF/` (appconfig-*.xml)
- **External Services**: Configured in `application.properties` with hostnames like `db01`, `mc01`, `rmq01`

## Key Patterns
- Service layer with interfaces (e.g., `UserService`) and implementations (e.g., `UserServiceImpl`)
- Spring Data JPA repositories extending `JpaRepository`
- Controllers use `@Autowired` for dependency injection
- Validation with custom validators and Hibernate Validator
- File uploads handled via `MultipartFile`

## Development Workflows
- **Build**: `mvn clean install -DskipTests` (produces WAR in target/)
- **Test**: `mvn test` (unit tests), `mvn verify -DskipUnitTests` (integration)
- **Local Dev**: Use Vagrant for multi-VM setup (`vagrant/Automated_provisioning_WinMacIntel/Vagrantfile`)
  - `db01`: MySQL (192.168.56.15)
  - `mc01`: Memcached (192.168.56.14)
  - `rmq01`: RabbitMQ (192.168.56.16)
  - `app01`: Tomcat (192.168.56.12)
- **Deploy**: Ansible playbooks in `ansible/` for production deployment
- **CI/CD**: Jenkins pipeline builds, tests, and publishes to Nexus

## Configuration
- Database schema in `src/main/resources/db_backup.sql`
- Application properties in `src/main/resources/application.properties`
- Logging via Logback (`logback.xml`)

## Conventions
- Package structure: `com.visualpathit.account.{controller,service,repository,model}`
- XML Spring config instead of annotations
- JSP views with Spring form tags
- BCrypt for password encoding
- Memcached for caching, RabbitMQ for messaging, Elasticsearch for search

## Common Tasks
- Adding new entities: Create JPA entity, repository interface, service interface/impl, controller
- External service integration: Update `application.properties` and corresponding service classes
- UI changes: Modify JSP files in `WEB-INF/views/`