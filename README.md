<!-- Git 仓库地址：git@github.com:rick-peng-li/react-express-appointment-app-web.git -->

# react-express-appointment-app-web

一个基于 React + Express + MongoDB 的预约管理示例项目，适用于诊所/门诊场景。项目包含用户预约流程与后台管理面板，支持服务展示、预约创建、预约状态管理、患者列表查看以及处方信息维护。

## 项目简介

本项目采用前后端分离结构：

- 前端负责展示官网首页、预约页面与后台 Dashboard。
- 后端提供预约、服务、处方相关接口。
- MongoDB 用于存储服务信息、预约记录与处方数据。
- 根目录脚本可统一安装依赖、分别启动前后端，适合本地开发和部署构建。

## 核心功能

- 首页展示诊所品牌内容与预约入口
- 服务列表展示与预约表单提交
- 后台查看预约列表、患者信息与统计信息
- 按日期筛选预约数据
- 更新预约状态与就诊状态
- 创建处方并维护药品信息

## 架构说明

### 整体结构

- `front-end/`：React 单页应用，负责页面渲染、路由与状态管理
- `back-end/`：Express API 服务，负责业务接口与数据库连接
- 根目录 `package.json`：统一管理安装、开发启动与前端构建脚本

### 前端技术栈

- React 16
- React Router
- Redux + Redux Thunk
- React Hook Form
- Bootstrap / React Bootstrap
- Material UI
- date-fns / moment
- Create React App

### 后端技术栈

- Node.js
- Express
- Mongoose
- MongoDB
- dotenv
- cors

### 前端页面与模块

- `/`：首页，展示头部导航、品牌内容与预约入口
- `/appointment`：预约页，展示服务项并提交预约
- `/dashboard`：后台页，包含 Dashboard、Appointment、Patients、Prescriptions 等模块
- Redux 模块主要包括：`alert`、`services`、`appointment`

### 后端接口模块

- `/api/appointment`
  - 服务创建与查询
  - 预约创建与查询
  - 预约状态更新
  - 就诊状态更新
- `/api/prescription`
  - 处方查询
  - 处方创建
  - 处方药品信息更新

## 目录结构

```text
react-express-appointment-app-web/
├─ back-end/                # Express 服务与 MongoDB 数据模型
│  ├─ models/               # Mongoose Schema
│  ├─ routers/api/          # API 路由
│  └─ server.js             # 后端入口
├─ front-end/               # React 前端应用
│  ├─ public/               # 静态资源
│  └─ src/
│     ├─ components/        # 业务组件
│     ├─ pages/             # 页面级组件
│     └─ redux/             # 状态管理
├─ .gitignore
├─ package.json             # 根目录脚本
└─ README.md
```

## 运行环境

建议使用以下环境启动项目：

- Node.js 14 及以上
- npm 6 及以上
- MongoDB 本地实例或 MongoDB Atlas

> 说明：项目内 `package.json` 声明的 Node 版本较旧（`v10.15.0`），这是原始配置；实际本地开发通常可以在更高版本 Node 环境下运行。如遇兼容问题，可优先切换到 Node 14 或 16 进行验证。

## 环境变量

后端通过 `dotenv` 读取环境变量，至少需要配置数据库连接地址。

可在 `back-end/` 下创建 `.env` 文件，例如：

```bash
MONGODB_URI=mongodb://127.0.0.1:27017/appointment_app
PORT=4000
NODE_ENV=development
```

前端 `package.json` 中已配置代理：

```text
proxy: http://localhost:4000
```

因此本地开发时，前端默认访问 `3000` 端口，接口请求会代理到后端 `4000` 端口。

## 安装依赖

在项目根目录执行：

```bash
npm install
npm run install-backEnd
npm run install-client
```

如果你希望分别安装，也可以进入 `back-end/` 与 `front-end/` 目录单独执行 `npm install`。

## 启动方式

### 方式一：前后端同时启动

在项目根目录执行：

```bash
npm run dev
```

启动后默认访问：

- 前端：http://localhost:3000
- 后端：http://localhost:4000

### 方式二：分别启动前后端

在项目根目录分别执行：

```bash
npm run server
npm run client
```

也可以进入子目录后分别启动：

```bash
cd back-end
npm start
```

```bash
cd front-end
npm start
```

## 构建与部署

前端生产构建：

```bash
npm run build
```

根目录还提供了面向部署场景的构建脚本：

```bash
npm run heroku-postbuild
```

该脚本会：

- 安装后端依赖
- 安装前端依赖
- 构建前端静态文件

## 开发说明

- 前端使用 `BrowserRouter` 管理页面路由
- 全局状态通过 Redux 管理，异步请求使用 Thunk
- 后端通过 Express Router 拆分预约与处方接口
- 数据层通过 Mongoose Schema 管理预约、服务与处方结构
- 生产环境下后端会尝试托管前端构建产物

## 注意事项

- 启动前请先确认 MongoDB 已可访问，且 `MONGODB_URI` 配置正确
- 如果前端无法获取接口数据，请优先检查后端是否运行在 `4000` 端口
- 当前项目中部分部署配置与代码细节保留了原始示例状态，若用于生产环境，建议进一步补充异常处理、鉴权、安全配置与部署脚本
