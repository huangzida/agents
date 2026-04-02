# 图标使用

使用 Iconify 图标库，支持数万种图标。

**官方文档**：https://doc.vben.pro/guide/advance/icon.html

**图标库**：https://icon-sets.iconify.design/

## 基础用法

```vue
<template>
  <!-- 使用 Iconify 图标 -->
  <Icon icon="lucide:home" class="size-5" />
  <Icon icon="mdi:account" class="size-5" />
</template>
```

## 常用图标集

### Lucide（推荐）

```vue
<template>
  <Icon icon="lucide:home" />
  <Icon icon="lucide:user" />
  <Icon icon="lucide:settings" />
  <Icon icon="lucide:search" />
  <Icon icon="lucide:plus" />
  <Icon icon="lucide:edit" />
  <Icon icon="lucide:trash-2" />
  <Icon icon="lucide:check" />
  <Icon icon="lucide:x" />
</template>
```

### Material Design

```vue
<template>
  <Icon icon="mdi:home" />
  <Icon icon="mdi:account" />
  <Icon icon="mdi:cog" />
</template>
```

## 菜单图标

```typescript
// 路由配置
meta: {
  icon: 'lucide:file-text',
}
```

## 动态图标

```vue
<script setup>
import { computed } from 'vue';

const props = defineProps<{
  status: 'success' | 'error' | 'warning';
}>();

const iconName = computed(() => {
  switch (props.status) {
    case 'success': return 'lucide:check-circle';
    case 'error': return 'lucide:x-circle';
    case 'warning': return 'lucide:alert-circle';
  }
});
</script>

<template>
  <Icon :icon="iconName" class="size-5" />
</template>
```

## 搜索图标

访问 [Iconify](https://icon-sets.iconify.design/) 搜索所需图标。
