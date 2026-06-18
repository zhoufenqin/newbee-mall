# Architecture Diagram

This document summarizes the high-level architecture and internal component relationships for newbee-mall.

## Application Architecture

```mermaid
flowchart TD
    subgraph Client["Client Layer"]
        Browser["Web Browser"]
        AdminUI["Admin UI"]
        MallUI["Mall UI"]
    end

    subgraph App["Application Layer - Spring Boot 2.7.5"]
        MVC["Spring MVC + Thymeleaf"]
        Interceptor["Login and Cart Interceptors"]
        Biz["Business Services"]
        MyBatis["MyBatis Mapper Layer"]
    end

    subgraph Data["Data Layer"]
        MySQL[("MySQL newbee_mall_db")]
        FileStore[("Local File Upload Directory")]
    end

    subgraph External["External Integrations"]
        BannerCDN["OSS Image Links"]
    end

    Browser -->|"HTTP requests"| MVC
    AdminUI -->|"admin operations"| MVC
    MallUI -->|"shopping workflows"| MVC
    MVC -->|"session checks"| Interceptor
    MVC -->|"delegates"| Biz
    Biz -->|"CRUD queries"| MyBatis
    MyBatis -->|"SQL"| MySQL
    MVC -->|"upload files"| FileStore
    MVC -->|"renders referenced assets"| BannerCDN
```

### Technology Stack Summary

| Layer | Technology | Version | Purpose |
|---|---|---|---|
| Presentation | Spring MVC, Thymeleaf | Spring Boot managed (2.7.5 BOM) | Server-side page rendering and request handling |
| Business | Spring Service components | Spring Boot managed | Order, cart, user, goods, and admin logic |
| Data Access | MyBatis Spring Boot Starter | 2.2.2 | Mapper-based persistence |
| Database | MySQL | runtime driver managed by Spring Boot BOM | Transactional data storage |
| Runtime | Java | 1.8 | Application runtime |

### Data Storage & External Services

The application stores business data in a single MySQL database (`newbee_mall_db`) and stores uploaded images/files in a local filesystem directory mapped under `/upload/**` and `/goods-img/**`. It also references external image URLs in seeded carousel/config data.

### Key Architectural Decisions

- Monolithic Spring Boot web application with both storefront and admin capabilities in one deployable unit.
- Layered architecture using Controllers -> Services -> MyBatis Mapper interfaces/XML.
- Session-based authentication and authorization checks implemented with MVC interceptors.

## Component Relationships

```mermaid
flowchart LR
    subgraph Presentation["Presentation"]
        AdminCtrl["Admin Controllers"]
        MallCtrl["Mall Controllers"]
        CommonCtrl["Common Controllers"]
    end

    subgraph Business["Business Logic"]
        AdminSvc["AdminUserServiceImpl"]
        UserSvc["NewBeeMallUserServiceImpl"]
        GoodsSvc["NewBeeMallGoodsServiceImpl"]
        CartSvc["NewBeeMallShoppingCartServiceImpl"]
        OrderSvc["NewBeeMallOrderServiceImpl"]
        CategorySvc["NewBeeMallCategoryServiceImpl"]
        IndexCfgSvc["NewBeeMallIndexConfigServiceImpl"]
        CarouselSvc["NewBeeMallCarouselServiceImpl"]
    end

    subgraph DataAccess["Data Access"]
        AdminMapper["AdminUserMapper"]
        UserMapper["MallUserMapper"]
        GoodsMapper["NewBeeMallGoodsMapper"]
        CartMapper["NewBeeMallShoppingCartItemMapper"]
        OrderMapper["NewBeeMallOrderMapper"]
        OrderItemMapper["NewBeeMallOrderItemMapper"]
        CategoryMapper["GoodsCategoryMapper"]
        IndexCfgMapper["IndexConfigMapper"]
        CarouselMapper["CarouselMapper"]
    end

    subgraph Infra["Infrastructure"]
        AdminInterceptor["AdminLoginInterceptor"]
        MallInterceptor["NewBeeMallLoginInterceptor"]
        CartInterceptor["NewBeeMallCartNumberInterceptor"]
        ExceptionHandler["NewBeeMallExceptionHandler"]
    end

    AdminCtrl -->|"delegates"| AdminSvc
    AdminCtrl -->|"delegates"| GoodsSvc
    AdminCtrl -->|"delegates"| CategorySvc
    AdminCtrl -->|"delegates"| OrderSvc
    AdminCtrl -->|"delegates"| UserSvc
    AdminCtrl -->|"delegates"| IndexCfgSvc
    AdminCtrl -->|"delegates"| CarouselSvc
    MallCtrl -->|"delegates"| UserSvc
    MallCtrl -->|"delegates"| GoodsSvc
    MallCtrl -->|"delegates"| CartSvc
    MallCtrl -->|"delegates"| OrderSvc
    CommonCtrl -->|"uploads and utility"| GoodsSvc

    AdminSvc -->|"queries"| AdminMapper
    UserSvc -->|"queries"| UserMapper
    GoodsSvc -->|"queries"| GoodsMapper
    CartSvc -->|"queries"| CartMapper
    CartSvc -->|"lookups"| GoodsMapper
    OrderSvc -->|"queries"| OrderMapper
    OrderSvc -->|"queries"| OrderItemMapper
    OrderSvc -->|"queries"| CartMapper
    OrderSvc -->|"updates stock"| GoodsMapper
    CategorySvc -->|"queries"| CategoryMapper
    IndexCfgSvc -->|"queries"| IndexCfgMapper
    CarouselSvc -->|"queries"| CarouselMapper

    AdminInterceptor -.->|"guards"| AdminCtrl
    MallInterceptor -.->|"guards"| MallCtrl
    CartInterceptor -.->|"injects cart count"| MallCtrl
    ExceptionHandler -.->|"handles exceptions"| Presentation
```

### Component Inventory

| Component | Layer | Type | Responsibility |
|---|---|---|---|
| `AdminController` + admin resource controllers | Presentation | MVC Controller | Back-office login and operational management |
| `PersonalController`, `GoodsController`, `ShoppingCartController`, `OrderController`, `IndexController` | Presentation | MVC Controller | Customer login, browsing, cart, and order flows |
| `NewBeeMallOrderServiceImpl` | Business | Service | Order lifecycle, stock updates, payment status transitions |
| `NewBeeMallShoppingCartServiceImpl` | Business | Service | Cart add/update/delete and cart snapshot composition |
| `NewBeeMallGoodsServiceImpl` | Business | Service | Product listing, search, and admin product management |
| `NewBeeMallUserServiceImpl` | Business | Service | Mall user registration, login, profile updates |
| `AdminUserServiceImpl` | Business | Service | Admin identity management |
| `*Mapper` interfaces + MyBatis XML | Data Access | Mapper | SQL execution and persistence mapping |
| `AdminLoginInterceptor`, `NewBeeMallLoginInterceptor`, `NewBeeMallCartNumberInterceptor` | Infrastructure | Interceptor | Session and page access control, cart count enrichment |
| `NewBeeMallExceptionHandler` | Infrastructure | Advice | Global exception mapping for JSON/view responses |
