# Modal/Drawer 组件

弹窗和抽屉组件，用于创建模态对话框和侧边抽屉。

**官方文档**：
- Modal: https://doc.vben.pro/components/common-ui/vben-modal.html
- Drawer: https://doc.vben.pro/components/common-ui/vben-drawer.html

**Playground**：`playground/src/views/examples/modal/`

## useVbenDrawer

抽屉组件，用于表单编辑等场景。

### 基础用法

```typescript
const [Drawer, drawerApi] = useVbenDrawer({
  title: '抽屉标题',
  onConfirm: () => {
    // 确认逻辑
  },
});
```

### 配合表单使用

```typescript
import { useVbenForm } from '#/adapter/form';

const [Form, formApi] = useVbenForm({ schema: [...] });

const [Drawer, drawerApi] = useVbenDrawer({
  connectedComponent: Form,
  onConfirm: async () => {
    const { valid } = await formApi.validate();
    if (!valid) return;
    const values = await formApi.getValues();
    // 保存数据
    drawerApi.close();
  },
});
```

### 常用配置

| 配置 | 说明 |
|------|------|
| `title` | 抽屉标题 |
| `connectedComponent` | 关联的组件 |
| `destroyOnClose` | 关闭时销毁内容 |
| `onConfirm` | 确认回调 |
| `onOpenChange` | 打开/关闭变化回调 |

### 抽屉 API

| 方法 | 说明 |
|------|------|
| `drawerApi.open()` | 打开抽屉 |
| `drawerApi.close()` | 关闭抽屉 |
| `drawerApi.lock()` | 锁定（禁用关闭） |
| `drawerApi.unlock()` | 解锁 |
| `drawerApi.setData(data)` | 设置数据 |

## useVbenModal

弹窗组件，用于信息展示、确认等场景。

### 基础用法

```typescript
const [Modal, modalApi] = useVbenModal({
  title: '弹窗标题',
  content: '弹窗内容',
});
```

### 确认弹窗

```typescript
const [Modal, modalApi] = useVbenModal({
  title: '确认操作',
  content: '确定要执行此操作吗？',
  onConfirm: () => {
    // 确认逻辑
  },
});
```

### 配合表单使用

```typescript
const [Modal, modalApi] = useVbenModal({
  connectedComponent: Form,
  onConfirm: async () => {
    const { valid } = await formApi.validate();
    if (!valid) return;
    // 保存数据
    modalApi.close();
  },
});
```

## Playground 示例

| 示例 | 路径 |
|------|------|
| 基础抽屉 | `examples/modal/drawer.vue` |
| 表单抽屉 | `examples/modal/drawer-form.vue` |
| 基础弹窗 | `examples/modal/modal.vue` |
| 确认弹窗 | `examples/modal/confirm.vue` |
