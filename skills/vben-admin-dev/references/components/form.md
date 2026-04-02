# 表单组件（useVbenForm）

vben-admin 提供的表单组件，基于 vee-validate，支持多种 UI 框架。

**官方文档**：https://doc.vben.pro/components/common-ui/vben-form.html

**Playground**：`playground/src/views/examples/form/`

## ⚠️ 重要规则：组件拆分

> **组件超过 500 行必须拆分！**

保持组件颗粒度细、易于维护和扩展：
- 将大组件拆分为多个小组件
- 每个组件职责单一
- 相关功能抽离为独立组件

### 拆分策略

| 场景 | 拆分方式 |
|------|----------|
| 表单 + 弹窗 | 使用 `useVbenForm` + `useVbenModal` |
| 复杂表单 | 按业务模块拆分为多个子表单 |
| 编辑详情 | 基本信息 + 物模型 等模块拆分 |

## 基础用法

### ❌ 错误做法：直接在 template 中写 Input 组件

```vue
<!-- ❌ 错误：在 template 中使用原生组件 -->
<template>
  <Input v-model="value" />
</template>

<script setup>
import { Input } from 'antdv-next';  // 这会导致运行时错误
</script>
```

### ✅ 正确做法：使用 schema 注册的组件

```vue
<!-- ✅ 正确：在 schema 中定义组件 -->
<script setup lang="ts">
import { useVbenForm } from '#/adapter/form';

const [Form, formApi] = useVbenForm({
  layout: 'horizontal',
  handleSubmit: (values) => {
    console.log('提交的值:', values);
  },
  schema: [
    {
      fieldName: 'username',
      label: '用户名',
      component: 'Input',
      rules: 'required',
    },
  ],
});
</script>

<template>
  <Form />
</template>
```

## useVbenForm + useVbenModal 组合

### ✅ 正确示例：弹窗表单

```vue
<script setup lang="ts">
import { useVbenModal } from '@vben/common-ui';
import { useVbenForm } from '#/adapter/form';

const [Form, formApi] = useVbenForm({
  handleSubmit: onSubmit,
  schema: [
    { component: 'Input', fieldName: 'name', label: '名称', rules: 'required' },
    { component: 'Select', fieldName: 'category', label: '分类' },
  ],
  showDefaultActions: false,
});

const [Modal, modalApi] = useVbenModal({
  fullscreenButton: false,
  onCancel() {
    modalApi.close();
  },
  onConfirm: async () => {
    await formApi.validateAndSubmitForm();
  },
  onOpenChange(isOpen) {
    if (isOpen) {
      const data = modalApi.getData();
      if (data) {
        formApi.setValues(data);
      }
    }
  },
  title: '弹窗标题',
});

function onSubmit(values) {
  // 处理提交
  modalApi.close();
}

function open(data) {
  modalApi.setData(data);
  modalApi.open();
}

defineExpose({ open });
</script>

<template>
  <Modal class="sm:w-[600px]">
    <Form />
  </Modal>
</template>
```

## ❌ 常见错误

### 错误1：在 template 中使用未注册的组件

```vue
<!-- ❌ 错误 -->
<template>
  <Button @click="handleClick">提交</Button>
  <Input v-model="value" />
</template>

<script setup>
import { Button, Input } from 'antdv-next';
</script>
```

**正确做法**：在 schema 中定义组件，或使用其他方式。

### 错误2：组件命名不规范

```vue
<!-- ❌ 错误：通用名称 -->
<script setup>
import Form from './Form.vue';  // Form 容易与其他组件冲突
</script>

<!-- ✅ 正确：语义化命名 -->
<script setup>
import AddProtocolModal from './AddProtocolModal.vue';
import UpdateProtocolModal from './UpdateProtocolModal.vue';
</script>
```

### 错误3：组件职责不清

```vue
<!-- ❌ 错误：一个大组件包含所有功能 -->
<!-- ProductEditModal.vue (1000+ 行) -->
<!-- - 基本信息编辑 -->
<!-- - 物模型配置 -->
<!-- - 文件上传 -->
<!-- - 审核流程 -->

<!-- ✅ 正确：按职责拆分 -->
<!-- ProductEditModal.vue - 弹窗容器 -->
<!-- ProductBasicInfo.vue - 基本信息 -->
<!-- ProductThingModel.vue - 物模型 -->
<!-- ProductAudit.vue - 审核流程 -->
```

## 布局配置

| 布局 | 说明 |
|------|------|
| `horizontal` | 水平布局（默认） |
| `vertical` | 垂直布局 |
| `inline` | 行内布局 |

## 字段类型

### 常用字段

| 组件 | 说明 |
|------|------|
| `Input` | 文本输入 |
| `InputPassword` | 密码输入 |
| `InputNumber` | 数字输入 |
| `Textarea` | 文本域 |
| `Select` | 下拉选择 |
| `ApiSelect` | 远程数据选择 |
| `TreeSelect` | 树形选择 |
| `DatePicker` | 日期选择 |
| `RangePicker` | 日期范围 |
| `TimePicker` | 时间选择 |
| `RadioGroup` | 单选组 |
| `CheckboxGroup` | 多选组 |
| `Switch` | 开关 |
| `Rate` | 评分 |
| `Cascader` | 级联选择 |
| `Upload` | 文件上传 |
| `IconPicker` | 图标选择 |

### 字段定义示例

```typescript
{
  fieldName: 'username',
  label: '用户名',
  component: 'Input',
  componentProps: {
    placeholder: '请输入用户名',
  },
  rules: 'required',
}
```

## 表单校验

### 预定义规则

- `required` - 输入项必填
- `selectRequired` - 选择项必填

### Zod 校验

```typescript
import { z } from '#/adapter/form';

{
  fieldName: 'username',
  rules: z.string()
    .min(2, '用户名至少2个字符')
    .max(20, '用户名最多20个字符'),
}
```

## 表单联动

使用 `dependencies` 实现字段联动：

```typescript
{
  fieldName: 'type',
  component: 'Select',
  // ...
},
{
  fieldName: 'conditionalField',
  component: 'Input',
  dependencies: {
    triggerFields: ['type'],
    show: (values) => values.type === 'specific',
    required: (values) => values.type === 'specific',
  },
}
```

## Form API

| 方法 | 说明 |
|------|------|
| `formApi.setFieldValue(name, value)` | 设置单个字段值 |
| `formApi.setValues(values)` | 设置多个字段值 |
| `formApi.getValues()` | 获取表单值 |
| `formApi.validate()` | 校验表单 |
| `formApi.resetForm()` | 重置表单 |
| `formApi.validateAndSubmitForm()` | 校验并提交 |
| `formApi.updateSchema(schema)` | 更新字段配置 |

## Playground 示例

| 示例 | 路径 |
|------|------|
| 基础表单 | `examples/form/basic.vue` |
| 查询表单 | `examples/form/query.vue` |
| 表单联动 | `examples/form/linkage.vue` |
| 表单校验 | `examples/form/rules.vue` |
| 弹窗表单 | `examples/modal/form-modal-demo.vue` |

### Textarea 字数统计（showCount）最佳实践
当 Textarea 组件启用 showCount: true 时，字数统计可能因父容器 overflow: hidden 而显示异常。
 ✅ 正确写法
使用 formItemClass 定义类名，配合 CSS 修复显示问题：

```typescript
{
  formItemClass: 'textarea-form-item',
  component: 'Textarea',
  componentProps: {
    maxlength: 200,
    showCount: true,
    rows: 3,
  },
  fieldName: 'description',
  label: '说明',
}
```

```typescript
<style scoped>
:deep(.textarea-form-item > div) {
  overflow: visible;
}
</style>
``` 

❌ 错误写法
直接在 wrapperClass 上设置样式（容易被覆盖，且作用域不精确）：

```typescript
{
  wrapperClass: 'custom-wrapper',
  component: 'Textarea',
  componentProps: { showCount: true },
}
```
注意 ：命名应使用 formItemClass 而非 wrapperClass ，因为 showCount 的后缀元素渲染在 formItem 内。