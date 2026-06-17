# Configuration & Externalized Settings Inventory

**newbee-mall** uses a single `application.properties` file as its only configuration source — there are no runtime profiles, no external config server, no secret store integration, and no environment variable overrides.

## Configuration Sources

| Source | Type | Path/Location | Notes |
|---|---|---|---|
| application.properties | Spring Boot application config | `src/main/resources/application.properties` | Single file; no profile-specific variants |
| Constants.java | Java compile-time constants | `src/main/java/ltd/newbee/mall/common/Constants.java` | Business constants (limits, keys) hardcoded in source |
| mapper XML files | MyBatis SQL mapping | `src/main/resources/mapper/*Mapper.xml` | SQL definitions; not runtime configuration |

No `bootstrap.properties`, `bootstrap.yml`, `application-*.yml` profile variants, Docker Compose files, Kubernetes manifests, `.env` files, Spring Cloud Config Server, Vault, Azure Key Vault, or AWS Secrets Manager references were found in the repository.

## Build Profiles

| Profile | Activation | Purpose | Key Dependencies/Plugins |
|---|---|---|---|
| (default) | Automatic | Standard Spring Boot JAR build | `spring-boot-maven-plugin` for executable JAR; no additional profiles declared |

No Maven build profiles (`<profiles>` block) are defined in `pom.xml`. The project uses only the default build lifecycle with the Spring Boot Maven Plugin.

## Runtime Profiles

| Profile | Activation Method | Config Files | Key Overrides |
|---|---|---|---|
| (default / none) | Implicit — no `spring.profiles.active` set | `application.properties` only | All settings in single file; no overrides |

No profile-specific configuration files (e.g., `application-dev.properties`, `application-prod.yml`) exist. There is no `spring.profiles.active` property configured. The application runs in a single fixed configuration regardless of environment.

## Properties Inventory

### newbee-mall — All Properties

| Property Key | Default Value | Profiles | Source |
|---|---|---|---|
| `server.port` | `28089` | (all) | application.properties |
| `spring.thymeleaf.cache` | `false` | (all) | application.properties |
| `spring.datasource.name` | `newbee-mall-datasource` | (all) | application.properties |
| `spring.datasource.driverClassName` | `com.mysql.cj.jdbc.Driver` | (all) | application.properties |
| `spring.datasource.url` | `jdbc:mysql://localhost:3306/newbee_mall_db?useUnicode=true&serverTimezone=Asia/Shanghai&characterEncoding=utf8&autoReconnect=true&useSSL=false&allowMultiQueries=true` | (all) | application.properties |
| `spring.datasource.username` | `root` | (all) | application.properties |
| `spring.datasource.password` | `[MASKED]` | (all) | application.properties |
| `spring.datasource.hikari.minimum-idle` | `5` | (all) | application.properties |
| `spring.datasource.hikari.maximum-pool-size` | `15` | (all) | application.properties |
| `spring.datasource.hikari.auto-commit` | `true` | (all) | application.properties |
| `spring.datasource.hikari.idle-timeout` | `10000` (ms) | (all) | application.properties |
| `spring.datasource.hikari.pool-name` | `hikariCP` | (all) | application.properties |
| `spring.datasource.hikari.max-lifetime` | `30000` (ms) | (all) | application.properties |
| `spring.datasource.hikari.connection-timeout` | `30000` (ms) | (all) | application.properties |
| `spring.datasource.hikari.connection-test-query` | `SELECT 1` | (all) | application.properties |
| `mybatis.mapper-locations` | `classpath:mapper/*Mapper.xml` | (all) | application.properties |

### Hardcoded Constants (Constants.java)

| Constant | Value | Purpose |
|---|---|---|
| `FILE_UPLOAD_DIC` | `D:\upload\` | Local filesystem upload directory (Windows path — requires change for Linux/cloud) |
| `INDEX_CAROUSEL_NUMBER` | `5` | Number of homepage carousel items |
| `INDEX_CATEGORY_NUMBER` | `10` | Max first-level categories on homepage |
| `SEARCH_CATEGORY_NUMBER` | `8` | Max first-level categories on search page |
| `INDEX_GOODS_HOT_NUMBER` | `4` | Hot-selling goods count on homepage |
| `INDEX_GOODS_NEW_NUMBER` | `5` | New arrivals count on homepage |
| `INDEX_GOODS_RECOMMOND_NUMBER` | `10` | Recommended goods count on homepage |
| `SHOPPING_CART_ITEM_TOTAL_NUMBER` | `13` | Max distinct items in a cart |
| `SHOPPING_CART_ITEM_LIMIT_NUMBER` | `5` | Max quantity per cart item |
| `GOODS_SEARCH_PAGE_LIMIT` | `10` | Default search results per page |
| `ORDER_SEARCH_PAGE_LIMIT` | `3` | Default orders per page in personal history |
| `MALL_VERIFY_CODE_KEY` | `mallVerifyCode` | Session key for CAPTCHA code |
| `MALL_USER_SESSION_KEY` | `newBeeMallUser` | Session key for logged-in user object |

## Startup Parameters & Resource Requirements

| Service | JVM/Runtime Options | Memory | Instance Count |
|---|---|---|---|
| newbee-mall | None documented (no startup scripts, no Dockerfile, no docker-compose.yml) | Not specified | 1 (single process) |

No JVM heap settings (`-Xms`/`-Xmx`), startup scripts, Dockerfiles, or container orchestration manifests are present in the repository. Resource allocation is entirely at the operator's discretion.

## Startup Dependency Chain

The application has a single external startup dependency: **MySQL** must be running and accepting connections at `localhost:3306` before the application starts. HikariCP will attempt to acquire a connection (timeout 30 s, test query `SELECT 1`) during startup. There is no health-check wait mechanism, no `dockerize`, no readiness probe, and no Spring Boot retry configuration — if MySQL is unavailable at startup time, the application will fail to start immediately.

```
MySQL (localhost:3306) → newbee-mall (port 28089)
```

No config server, discovery server, or message broker startup dependencies exist.

## Secrets & Sensitive Configuration

| Secret Reference | Type | Storage |
|---|---|---|
| `spring.datasource.url` | JDBC connection string (includes server address and DB name) | Plaintext in `application.properties` committed to source control |
| `spring.datasource.username` | Database username (`root`) | Plaintext in `application.properties` committed to source control |
| `spring.datasource.password` | Database password | Plaintext value (`[MASKED]`) in `application.properties` committed to source control |

### Secrets Provisioning Workflow

**No secrets management workflow exists.** All sensitive values (database credentials) are stored in plaintext in `application.properties`, which is committed directly to the source repository. There is no integration with any secret store (HashiCorp Vault, Azure Key Vault, AWS Secrets Manager), no environment variable substitution pattern (`${ENV_VAR}`), no encrypted property support (Jasypt), and no CI/CD pipeline-injected secrets.

To deploy this application securely, operators must manually edit `application.properties` with production credentials before packaging. This is a significant security risk: credentials are version-controlled alongside the application code.

## Feature Flags

No feature flag framework (LaunchDarkly, Unleash, Spring Feature Flags) is used. There are no `@ConditionalOnProperty` or `@ConditionalOnExpression` annotations in the codebase. Business limits (cart size, displayed items counts) are hardcoded in `Constants.java` and cannot be changed at runtime without a code change and redeployment.

## Framework & Runtime Versions

| Component | Version | Source |
|---|---|---|
| Java (target) | 1.8 (Java 8) | `pom.xml` `<java.version>` |
| Spring Boot | 2.7.5 | `pom.xml` `<parent>` |
| Spring MVC | 5.3.x (managed by Spring Boot 2.7.5) | Spring Boot BOM |
| Thymeleaf | 3.0.x (managed by Spring Boot 2.7.5) | Spring Boot BOM |
| Spring Session Core | 2.7.x (managed by Spring Boot 2.7.5) | Spring Boot BOM |
| MyBatis Spring Boot Starter | 2.2.2 | `pom.xml` explicit |
| HikariCP | 4.x (managed by Spring Boot 2.7.5) | Spring Boot BOM |
| mysql-connector-java | Managed by Spring Boot BOM | `pom.xml` (runtime scope, no explicit version) |
| hutool-captcha | 5.8.7 | `pom.xml` explicit |
| Maven | 3.x (no wrapper) | Build tool |
| Spring Boot Maven Plugin | 2.7.5 | `pom.xml` `<build><plugins>` |
