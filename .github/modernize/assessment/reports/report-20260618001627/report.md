# newbee-mall

## Summary

| Metric | Value |
|--------|-------|
| Total Issues | 14 |
| Mandatory Blockers | 9 |
| Potential Issues | 5 |

## Component Information

| Property | Value |
|----------|-------|
| Language | Java, JavaScript |
| Frameworks | Spring Boot, Spring |
| Build tools | Maven |
| JDK version | 1.8 |

## Cloud Readiness Issues

| Issue Name | Criticality | Story Points | Occurrences |
|------------|-------------|--------------|-------------|
| File system - java.net.URL/URI | Mandatory | 3 | [3](#File_system_-_java_net_URL_URI) |
| CRA: Use of weak hash algorithm MD5 | Mandatory | 5 | [2](#CRA_Use_of_weak_hash_algorithm_MD5) |
| CRA: Use of insecure random number generator java.util.Random | Mandatory | 5 | [2](#CRA_Use_of_insecure_random_number_generator_java_util_Random) |
| Local JDBC Calls | Mandatory | 5 | [1](#Local_JDBC_Calls) |
| No Dockerfile found | Mandatory | 3 | 1 |
| CRA: Default or well-known password detected | Mandatory | 3 | [1](#CRA_Default_or_well-known_password_detected) |
| File system - Java IO | Mandatory | 3 | [1](#File_system_-_Java_IO) |
| HTTP Session data storage | Potential | 5 | [14](#HTTP_Session_data_storage) |
| MySQL database found | Potential | 5 | [2](#MySQL_database_found) |
| Password found in configuration file | Potential | 3 | [1](#Password_found_in_configuration_file) |
| Server port configuration found | Potential | 1 | [1](#Server_port_configuration_found) |
| CRA: Use of Math.random() which is not cryptographically secure | Potential | 3 | [1](#CRA_Use_of_Math_random_which_is_not_cryptographically_secure) |

### Issue Details

<details id="File_system_-_java_net_URL_URI">
<summary><b>File system - java.net.URL/URI</b> — affected files</summary>

- `src/main/java/ltd/newbee/mall/controller/common/UploadController.java (line 75)`
- `src/main/java/ltd/newbee/mall/controller/common/UploadController.java (line 130)`
- `src/main/java/ltd/newbee/mall/util/NewBeeMallUtils.java (line 15)`

</details>

<details id="CRA_Use_of_weak_hash_algorithm_MD5">
<summary><b>CRA: Use of weak hash algorithm MD5</b> — affected files</summary>

- `src/main/java/ltd/newbee/mall/util/SystemUtil.java (line 29)`
- `src/main/java/ltd/newbee/mall/util/MD5Util.java (line 34)`

</details>

<details id="CRA_Use_of_insecure_random_number_generator_java_util_Random">
<summary><b>CRA: Use of insecure random number generator java.util.Random</b> — affected files</summary>

- `src/main/java/ltd/newbee/mall/controller/common/UploadController.java (line 60)`
- `src/main/java/ltd/newbee/mall/controller/common/UploadController.java (line 116)`

</details>

<details id="Local_JDBC_Calls">
<summary><b>Local JDBC Calls</b> — affected files</summary>

- `src/main/resources/application.properties (line 10)`

</details>

<details id="CRA_Default_or_well-known_password_detected">
<summary><b>CRA: Default or well-known password detected</b> — affected files</summary>

- `src/main/resources/application.properties (line 12)`

</details>

<details id="File_system_-_Java_IO">
<summary><b>File system - Java IO</b> — affected files</summary>

- `src/main/java/ltd/newbee/mall/controller/common/UploadController.java (line 29)`

</details>

<details id="HTTP_Session_data_storage">
<summary><b>HTTP Session data storage</b> — affected files</summary>

- `src/main/java/ltd/newbee/mall/controller/admin/AdminController.java (line 60)`
- `src/main/java/ltd/newbee/mall/controller/admin/AdminController.java (line 64)`
- `src/main/java/ltd/newbee/mall/controller/admin/AdminController.java (line 69)`
- `src/main/java/ltd/newbee/mall/controller/admin/AdminController.java (line 74)`
- `src/main/java/ltd/newbee/mall/controller/admin/AdminController.java (line 75)`
- `src/main/java/ltd/newbee/mall/controller/admin/AdminController.java (line 80)`
- `src/main/java/ltd/newbee/mall/service/impl/NewBeeMallUserServiceImpl.java (line 70)`
- `src/main/java/ltd/newbee/mall/service/impl/NewBeeMallUserServiceImpl.java (line 93)`
- `src/main/java/ltd/newbee/mall/controller/admin/AdminController.java (line 22)`
- `src/main/java/ltd/newbee/mall/controller/mall/OrderController.java (line 32)`
- `src/main/java/ltd/newbee/mall/controller/mall/PersonalController.java (line 26)`
- `src/main/java/ltd/newbee/mall/controller/mall/ShoppingCartController.java (line 27)`
- `src/main/java/ltd/newbee/mall/service/NewBeeMallUserService.java (line 16)`
- `src/main/java/ltd/newbee/mall/service/impl/NewBeeMallUserServiceImpl.java (line 22)`

</details>

<details id="MySQL_database_found">
<summary><b>MySQL database found</b> — affected files</summary>

- `src/main/resources/application.properties (line 10)`

</details>

<details id="Password_found_in_configuration_file">
<summary><b>Password found in configuration file</b> — affected files</summary>

- `src/main/resources/application.properties (line 12)`

</details>

<details id="Server_port_configuration_found">
<summary><b>Server port configuration found</b> — affected files</summary>

- `src/main/resources/application.properties (line 6)`

</details>

<details id="CRA_Use_of_Math_random_which_is_not_cryptographically_secure">
<summary><b>CRA: Use of Math.random() which is not cryptographically secure</b> — affected files</summary>

- `src/main/java/ltd/newbee/mall/util/NumberUtil.java (line 38)`

</details>

## Upgrade Issues

| Issue Name | Criticality | Story Points | Occurrences |
|------------|-------------|--------------|-------------|
| The java.annotation (Common Annotations) module has been removed from OpenJDK 11 | Mandatory | 2 | [13](#The_java_annotation_Common_Annotations_module_has_been_removed_from_OpenJDK_11) |
| Java Version Has Reached the End of Support | Mandatory | 8 | [1](#Java_Version_Has_Reached_the_End_of_Support) |

### Issue Details

<details id="The_java_annotation_Common_Annotations_module_has_been_removed_from_OpenJDK_11">
<summary><b>The java.annotation (Common Annotations) module has been removed from OpenJDK 11</b> — affected files</summary>

- `src/main/java/ltd/newbee/mall/controller/admin/AdminController.java (line 20)`
- `src/main/java/ltd/newbee/mall/controller/admin/NewBeeMallCarouselController.java (line 22)`
- `src/main/java/ltd/newbee/mall/controller/admin/NewBeeMallGoodsCategoryController.java (line 25)`
- `src/main/java/ltd/newbee/mall/controller/admin/NewBeeMallGoodsController.java (line 28)`
- `src/main/java/ltd/newbee/mall/controller/admin/NewBeeMallGoodsIndexConfigController.java (line 24)`
- `src/main/java/ltd/newbee/mall/controller/admin/NewBeeMallOrderController.java (line 24)`
- `src/main/java/ltd/newbee/mall/controller/admin/NewBeeMallUserController.java (line 20)`
- `src/main/java/ltd/newbee/mall/controller/mall/GoodsController.java (line 28)`
- `src/main/java/ltd/newbee/mall/controller/mall/IndexController.java (line 24)`
- `src/main/java/ltd/newbee/mall/controller/mall/OrderController.java (line 30)`
- `src/main/java/ltd/newbee/mall/controller/mall/PersonalController.java (line 24)`
- `src/main/java/ltd/newbee/mall/controller/mall/ShoppingCartController.java (line 25)`
- `src/main/java/ltd/newbee/mall/service/impl/AdminUserServiceImpl.java (line 17)`

</details>

<details id="Java_Version_Has_Reached_the_End_of_Support">
<summary><b>Java Version Has Reached the End of Support</b> — affected files</summary>

- `pom.xml (line 26)`

</details>

---

## Codebase Insights

> **Note:** These documents are generated by AI and may contain inaccuracies or incomplete information. Please review carefully.

1. **[Architecture Diagram](facts/architecture-diagram.md)** — Understand the big picture: system layers and component relationships
2. **[Dependency Map](facts/dependency-map.md)** — Know what the project depends on and where the risks are
3. **[API & Service Contracts](facts/api-service-contracts.md)** — See how services communicate and what contracts they expose
4. **[Data Architecture](facts/data-architecture.md)** — Explore data models, storage, and data flow patterns
5. **[Configuration Inventory](facts/configuration-inventory.md)** — Review how the application is configured across environments
6. **[Business Workflows](facts/business-workflows.md)** — Trace end-to-end business processes and domain logic

[Share feedback](https://aka.ms/ghcp-appmod/feedback)
