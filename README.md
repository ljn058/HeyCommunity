
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
| 认证授权      | Sa-Token 1.42                        |
| 缓存          | Redis 7.0（动态流缓存、计数器）                                         |
| 多媒体        | Hutool 图片处理 + FFmpeg 视频转码 + 微信内容安全 SDK                    |
| 构建工具      | Maven 3.9                                    |


## 📁 目录结构（核心模块）
```
heycommunity-backend/
├── post-service          # 动态服务（核心模块）
│   ├── src/main/java/com/heycommunity/post
│   │   ├── controller  # REST API 控制器
│   │   ├── service     # 业务逻辑（含微信审核）
│   │   ├── entity      # JPA 实体（@Entity）
│   │   └── repository  # 数据仓库（@Repository）
│   └── resources/db/migration  # Flyway 迁移文件（V1__init.sql）
├── admin-service         # 管理后台（前后端分离）
│   ├── src/main/java/com/heycommunity/admin
│   │   └── config      # Spring Security 权限配置
│   └── src/main/resources/static  # 管理界面静态资源（Vue3 构建产物）
├── common-entity         # 共享实体模块（通过 Maven 依赖）
├── file-service          # 独立文件服务（支持 OSS 直传）
└── docs                  # 架构文档、接口文档（Swagger 自动生成）
```

## 📝 版本路线图
| 版本   | 目标功能                                  | 预计时间   |
|--------|-----------------------------------------|------------|
| v1.0.0 | 完成核心模块迁移（动态/用户/评论）        | 2025-10    |


> 本项目采用 MIT 协议。  
> Copyright © 2025-present HeyCommunity Contributors
