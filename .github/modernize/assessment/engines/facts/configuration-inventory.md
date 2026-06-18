# Configuration & Externalized Settings Inventory

This inventory summarizes configuration sources and externalized settings for newbee-mall, including runtime properties, profile behavior, and sensitive configuration handling.

## Configuration Sources

| Source | Type | Path/Location | Notes |
|---|---|---|---|
| Spring application properties | file | `src/main/resources/application.properties` | Primary runtime configuration source |
| MyBatis mapper config | property reference | `mybatis.mapper-locations` in `application.properties` | Points to XML SQL mappings |
| Maven build descriptor | file | `pom.xml` | Dependency and build plugin management |
| Schema bootstrap SQL | file | `src/main/resources/newbee_mall_schema.sql` | DB schema and seed data script |

## Build Profiles

| Profile | Activation | Purpose | Key Dependencies/Plugins |
|---|---|---|---|
| Default Maven build | Standard `mvn` lifecycle | Compile/package Spring Boot jar | `spring-boot-maven-plugin` |

No custom Maven `<profiles>` were detected.

## Runtime Profiles

| Profile | Activation Method | Config Files | Key Overrides |
|---|---|---|---|
| default | implicit (no `spring.profiles.active`) | `application.properties` | datasource, server port, hikari pool settings |

No profile-specific files (`application-dev.properties`, etc.) were detected.

## Properties Inventory

| Property Key | Default | Profiles | Source |
|---|---|---|---|
| `server.port` | `28089` | default | `application.properties` |
| `spring.thymeleaf.cache` | `false` | default | `application.properties` |
| `spring.datasource.name` | `newbee-mall-datasource` | default | `application.properties` |
| `spring.datasource.driverClassName` | `com.mysql.cj.jdbc.Driver` | default | `application.properties` |
| `spring.datasource.url` | JDBC URL to localhost MySQL | default | `application.properties` |
| `spring.datasource.username` | `root` | default | `application.properties` |
| `spring.datasource.password` | `[MASKED]` | default | `application.properties` |
| `spring.datasource.hikari.minimum-idle` | `5` | default | `application.properties` |
| `spring.datasource.hikari.maximum-pool-size` | `15` | default | `application.properties` |
| `spring.datasource.hikari.auto-commit` | `true` | default | `application.properties` |
| `spring.datasource.hikari.idle-timeout` | `10000` | default | `application.properties` |
| `spring.datasource.hikari.pool-name` | `hikariCP` | default | `application.properties` |
| `spring.datasource.hikari.max-lifetime` | `30000` | default | `application.properties` |
| `spring.datasource.hikari.connection-timeout` | `30000` | default | `application.properties` |
| `spring.datasource.hikari.connection-test-query` | `SELECT 1` | default | `application.properties` |
| `mybatis.mapper-locations` | `classpath:mapper/*Mapper.xml` | default | `application.properties` |

## Startup Parameters & Resource Requirements

| Service | JVM/Runtime Options | Memory | Instance Count |
|---|---|---|---|
| newbee-mall | Not specified in repository launch scripts/config | Not specified | Not specified |

No explicit `-Xms/-Xmx`, container limits, or scaling settings were found in this repository.

## Startup Dependency Chain

1. MySQL database must be reachable at configured JDBC endpoint.
2. `newbee-mall` starts, initializes datasource and MyBatis mappers.
3. Web endpoints become available once Spring Boot context initialization completes.

No explicit wait-for scripts, readiness probes, or orchestrator dependency definitions were detected.

## Secrets & Sensitive Configuration

| Secret Reference | Type | Storage (masked) |
|---|---|---|
| `spring.datasource.password` | Database credential | `application.properties` value masked |
| `spring.datasource.username` | Database account | plaintext config value |

### Secrets Provisioning Workflow

In the current repository, secrets are file-based and loaded directly from `application.properties` at startup. No external secret manager integration (Vault/KeyVault/Secrets Manager) or managed identity flow was identified. Service startup binds datasource credentials immediately for DB connectivity.

## Feature Flags

| Flag Name | Default | Controlled By |
|---|---|---|
| No explicit feature flags detected | N/A | N/A |

Conditional feature frameworks (`@ConditionalOnProperty`, LaunchDarkly, Unleash, etc.) were not found.

## Framework & Runtime Versions

| Component | Version | Source |
|---|---|---|
| Spring Boot | 2.7.5 | `pom.xml` parent |
| Java target | 1.8 | `pom.xml` property |
| MyBatis Spring Boot Starter | 2.2.2 | `pom.xml` property/dependency |
| hutool-captcha | 5.8.7 | `pom.xml` property/dependency |
| Maven plugin | spring-boot-maven-plugin (managed) | `pom.xml` |
| MySQL JDBC driver | managed by Spring Boot BOM | `pom.xml` dependency |
