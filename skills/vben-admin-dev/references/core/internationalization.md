# 国际化配置

项目国际化文件位于 `src/locales/` 目录。

**官方文档**：https://doc.vben.pro/guide/advance/i18n.html

## 语言包结构

```
src/locales/
└── langs/
    ├── zh-CN/
    │   ├── common.json     # 公共翻译
    │   └── system.json     # 系统翻译
    └── en-US/
        ├── common.json
        └── system.json
```

## 定义翻译

```json
// src/locales/langs/zh-CN/example.json
{
  "title": "示例",
  "list": {
    "title": "列表",
    "search": "搜索",
    "create": "创建",
    "edit": "编辑",
    "delete": "删除"
  }
}
```

## 使用翻译

```vue
<script setup>
import { $t } from '#/locales';
</script>

<template>
  <span>{{ $t('example.title') }}</span>
</template>
```

## 切换语言

```typescript
import { useLocale } from '@vben/locales';

const { locale } = useLocale();

// 切换到中文
locale.value = 'zh-CN';

// 切换到英文
locale.value = 'en-US';
```

## 动态语言包

```typescript
import { loadLocaleAsync } from '@vben/locales';

await loadLocaleAsync('zh-CN', () =>
  import('./langs/zh-CN/example.json'),
);
```
