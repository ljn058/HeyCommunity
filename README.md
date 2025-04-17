
# HeyCommunity 后端服务（Spring Boot 版）
## 项目定位
**HeyCommunity-backend** 是 **HeyCommunity 社区平台**的**核心后端服务**，基于 **Spring Boot 3.2+** 重构，提供：
- **多端 API**（小程序/Web/Admin）
- **可视化管理后台**（内容审核、用户管理、系统配置）
- **社区核心功能**（动态发布、互动、多媒体存储）

> 原 Laravel 版本：https://github.com/HeyCommunity/HeyCommunity  
> 前端仓库：https://github.com/HeyCommunity/HeyCommunity-frontend


## 🌟 核心功能
| 模块                | 功能亮点                                                                 |
|---------------------|--------------------------------------------------------------------------|
| **动态系统**        | 图文/视频动态发布、内容安全检测（微信接口）、智能排序（Redis+MySQL）     |
| **后台管理**        | RBAC 权限系统、数据看板、可视化配置（如跑马灯、轮播图）                 |
| **多媒体服务**      | 阿里云OSS存储、视频元数据解析、图片智能裁剪                      |
| **互动体系**        | 点赞/收藏/评论多级回复、通知推送                        |
| **安全防护**        | 鉴权认证、SQL 注入防护、内容违规自动拦截（微信风控接口）                |


## 🚀 技术栈（Spring Boot 版）
| 分类          | 技术选型                                                                 |
|---------------|--------------------------------------------------------------------------|
| 框架          | Spring Boot 3.2                    |
| 持久化        | MyBatis-Plus + MySQL8        |
| 认证授权      | Sa - Token 1.42                        |
| 缓存          | Redis 7.0（动态流缓存、计数器）                                         |
| 多媒体        | Hutool 图片处理 + FFmpeg 视频转码 + 微信内容安全 SDK                    |
| 构建工具      | Maven 3.9                                    |
| 后台前端      | Vue3 + Element UI Plus                          |

## 📁 目录结构（核心模块）
```java
heycommunity
├── post-service          # 动态服务（核心模块）
│   ├── src
│   │   ├── main
│   │   │   ├── java
│   │   │   │   └── com
│   │   │   │       └── heycommunity
│   │   │   │           └── post
│   │   │   │               ├── controller  # REST API 控制器，遵循单一职责原则
│   │   │   │               ├── dto         # 数据传输对象，用于接口数据传递
│   │   │   │               ├── service     # 业务逻辑层（含微信审核）
│   │   │   │               │   ├── impl    # 业务逻辑实现类
│   │   │   │               ├── entity      # 数据库实体类，与 MyBatis-Plus 映射
│   │   │   │               ├── mapper      # MyBatis-Plus 映射器接口
│   │   │   │               ├── config      # 配置类，如数据库连接、MyBatis-Plus 配置等
│   │   │   │               ├── exception   # 自定义异常类
│   │   │   │               ├── util        # 工具类
│   │   │   │               └── aspect      # AOP 切面类，用于日志、权限等
│   │   │   └── resources
│   │   │       ├── application.yml         # 主配置文件
│   │   │       ├── mapper                  # MyBatis-Plus XML 映射文件（如果有）
│   │   │       └── db
│   │   │           └── migration           # Flyway 迁移文件（V1__init.sql）
│   │   └── test                            # 测试代码
│   │       └── java
│   │           └── com
│   │               └── heycommunity
│   │                   └── post
│   │                       ├── controller  # 控制器测试类
│   │                       ├── service     # 服务层测试类
│   │                       └── mapper      # 映射器测试类
├── admin-service         # 管理后台（前后端分离）
│   ├── src
│   │   ├── main
│   │   │   ├── java
│   │   │   │   └── com
│   │   │   │       └── heycommunity
│   │   │   │           └── admin
│   │   │   │               ├── controller  # REST API 控制器
│   │   │   │               ├── service     # 业务逻辑层
│   │   │   │               │   ├── impl    # 业务逻辑实现类
│   │   │   │               ├── config      # Spring Security 权限配置
│   │   │   │               ├── dto         # 数据传输对象
│   │   │   │               ├── entity      # 数据库实体类，与 MyBatis-Plus 映射
│   │   │   │               ├── mapper      # MyBatis-Plus 映射器接口
│   │   │   │               └── util        # 工具类
│   │   │   └── resources
│   │   │       ├── application.yml         # 主配置文件
│   │   │       └── static                  # 管理界面静态资源（Vue3 + Element UI Plus 构建产物）
│   │   └── test                            # 测试代码
│   │       └── java
│   │           └── com
│   │               └── heycommunity
│   │                   └── admin
│   │                       ├── controller  # 控制器测试类
│   │                       ├── service     # 服务层测试类
│   │                       └── mapper      # 映射器测试类
│   └── frontend                            # 新增：后台前端项目目录
│       ├── src
│       │   ├── assets                      # 静态资源
│       │   ├── components                  # 公共组件
│       │   ├── views                       # 页面视图
│       │   ├── router                      # 路由配置
│       │   ├── store                       # Vuex 状态管理
│       │   ├── api                         # 接口请求封装
│       │   ├── utils                       # 工具函数
│       │   ├── App.vue                     # 根组件
│       │   └── main.js                     # 入口文件
│       ├── public
│       │   └── index.html                  # 首页模板
│       ├── .gitignore
│       ├── package.json
│       ├── vue.config.js                   # Vue 项目配置文件
│       └── README.md
├── common-entity         # 共享实体模块（通过 Maven 依赖）
│   ├── src
│   │   ├── main
│   │   │   ├── java
│   │   │   │   └── com
│   │   │   │       └── heycommunity
│   │   │   │           └── entity          # 共享实体类，与 MyBatis-Plus 映射
│   │   │   └── resources
│   │   │       └── application.yml         # 主配置文件
│   │   └── test                            # 测试代码
│   │       └── java
│   │           └── com
│   │               └── heycommunity
│   │                   └── entity          # 实体类测试类
├── file-service          # 独立文件服务（支持 OSS 直传）
│   ├── src
│   │   ├── main
│   │   │   ├── java
│   │   │   │   └── com
│   │   │   │       └── heycommunity
│   │   │   │           └── file
│   │   │   │               ├── controller  # REST API 控制器
│   │   │   │               ├── service     # 业务逻辑层
│   │   │   │               │   ├── impl    # 业务逻辑实现类
│   │   │   │               ├── config      # 配置类，如 OSS 配置、MyBatis-Plus 配置
│   │   │   │               ├── dto         # 数据传输对象
│   │   │   │               ├── entity      # 数据库实体类，与 MyBatis-Plus 映射
│   │   │   │               ├── mapper      # MyBatis-Plus 映射器接口
│   │   │   │               └── util        # 工具类
│   │   │   └── resources
│   │   │       ├── application.yml         # 主配置文件
│   │   │       └── mapper                  # MyBatis-Plus XML 映射文件（如果有）
│   │   └── test                            # 测试代码
│   │       └── java
│   │           └── com
│   │               └── heycommunity
│   │                   └── file
│   │                       ├── controller  # 控制器测试类
│   │                       ├── service     # 服务层测试类
│   │                       └── mapper      # 映射器测试类
└── docs                  # 架构文档、接口文档（Swagger 自动生成）
```

## 📝 版本路线图
| 版本   | 目标功能                                  | 预计时间   |
|--------|-----------------------------------------|------------|
| v1.0.0 | 完成核心模块迁移（动态/用户/评论）        | 2025-10    |


> 本项目采用 MIT 协议。  
> Copyright © 2025-present HeyCommunity Contributors
