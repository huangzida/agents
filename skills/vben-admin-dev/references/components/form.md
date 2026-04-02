# 表单组件（useVbenForm）

vben-admin 提供的表单组件，基于 vee-validate，支持多种 UI 框架。

**官方文档**：https://doc.vben.pro/components/common-ui/vben-form.html

**Playground**：`playground/src/views/examples/form/`

## 基础用法

```vue
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
| `formApi.updateSchema(schema)` | 更新字段配置 |

## Playground 示例

| 示例 | 路径 |
|------|------|
| 基础表单 | `examples/form/basic.vue` |
| 查询表单 | `examples/form/query.vue` |
| 表单联动 | `examples/form/linkage.vue` |
| 表单校验 | `examples/form/rules.vue` |
