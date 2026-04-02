# 项目结构

## Monorepo 结构

```
api-admin/
├── apps/              # 应用目录
│   ├── playground/   # 示例和演示 ⭐
│   ├── web-antd/     # Ant Design Vue
│   ├── web-ele/      # Element Plus
│   └── web-naive/    # Naive UI
├── packages/         # 共享包
│   ├── @core/        # 核心包
│   │   ├── base/     # 基础包
│   │   ├── ui-kit/   # UI 组件包
│   │   └── layouts/  # 布局包
│   ├── effects/       # 功能包
│   │   ├── access/   # 权限控制
│   │   ├── hooks/    # 钩子函数
│   │   └── layouts/  # 布局功能
│   ├── stores/       # 状态管理
│   ├── locales/      # 国际化
│   └── utils/        # 工具函数
├── docs/             # 文档
└── internal/         # 内部工具配置
```

## Playground 结构

```
apps/playground/src/
├── adapter/          # 组件适配器
├── api/              # API 接口
├── components/       # 公共组件
├── hooks/            # 组合式函数
├── locales/          # 国际化
├── router/           # 路由配置
├── stores/           # 状态管理
├── styles/           # 全局样式
├── utils/            # 工具函数
└── views/            # 页面视图
    ├── _core/        # 核心页面
    ├── demos/        # 演示
    └── examples/     # 示例
```

## 路径别名

| 别名 | 路径 |
|------|------|
| `#/` | `src/` |
| `#@` | 源代码根目录 |
| `#/api` | `src/api` |
| `#/adapter` | `src/adapter` |
| `#/locales` | `src/locales` |
| `#/store` | `src/store` |
