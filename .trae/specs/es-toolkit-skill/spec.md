# es-toolkit 技能规格

## 为什么需要这个技能

es-toolkit 是一个现代 JavaScript 实用工具库，提供了经过优化的函数来替代 lodash。相比 lodash，es-toolkit 体积减少高达 97%，运行速度快 2-3 倍。它支持 TypeScript，拥有 100% 的测试覆盖率。在编写或重构 JavaScript/TypeScript 代码时，经常需要快速查阅 es-toolkit 的 API 文档。

官方文档：https://es-toolkit.dev/
AI 集成文档：https://es-toolkit.dev/llms.txt

## 需求变更

- **新增**：创建 `es-toolkit` 技能，用于在编写/重构 JavaScript/TypeScript 代码时提供 es-toolkit 文档参考

## 影响范围

- **新增技能**：`es-toolkit` 技能将添加到 `.trae/skills/` 目录
- **文档来源**：基于 es-toolkit 官方文档 (https://es-toolkit.dev/)
- **离线参考**：技能将包含关键 API 的离线参考文档

## 新增需求

### 需求：es-toolkit 技能

当用户编写 JavaScript/TypeScript 代码时，此技能应提供 es-toolkit 函数的快速参考。

#### 触发场景

- **当** 用户需要处理数组操作（如去重、分组、查找）
- **当** 用户需要处理对象操作（如合并、取值、转换）
- **当** 用户需要使用函数式编程工具（如防抖、节流、缓存）
- **当** 用户需要数学运算（如舍入、限制范围、随机数）
- **当** 用户需要 Promise 操作（如延迟、重试、并发控制）
- **当** 用户需要字符串操作（如截断、驼峰转换、模板填充）
- **当** 用户需要类型检查（如 isNil、isString、isArray）
- **当** 用户需要使用 lodash 的高性能替代方案
- **当** 用户被明确要求扫描代码库以使用 es-toolkit 替代自定义实现
- **则** 提供 es-toolkit 函数推荐，包括函数签名、使用示例和性能对比

#### 代码审查场景

- **当** 审查代码时发现可能存在可以用 es-toolkit 优化的自定义实现
- **则** 标记潜在优化点并提供 es-toolkit 函数建议

## es-toolkit 函数分类索引

### 1. Array 函数 (数组操作)

| 函数 | 功能 | 兼容性 |
| --- | --- | --- |
| chunk | 将数组分成指定大小的块 | compat |
| compact | 移除假值（false, null, 0, '', undefined, NaN） | compat |
| concat | 连接数组 | compat |
| difference | 返回差异元素 | compat |
| differenceBy | 按函数计算差异 | compat |
| differenceWith | 按比较器计算差异 | compat |
| drop | 删除前 n 个元素 | compat |
| dropRight | 删除后 n 个元素 | compat |
| dropRightWhile | 从右边删除满足条件的元素 | compat |
| dropWhile | 删除满足条件的元素 | compat |
| fill | 填充数组 | compat |
| filter | 过滤元素 | compat |
| filterAsync | 异步过滤 | - |
| find | 查找第一个匹配元素 | compat |
| flatMap | 扁平化映射 | compat |
| flatMapAsync | 异步扁平化映射 | - |
| flatMapDeep | 完全扁平化映射 | compat |
| flatten | 扁平化一层 | compat |
| flattenDeep | 完全扁平化 | compat |
| flattenObject | 扁平化对象 | - |
| forEach | 遍历 | compat |
| forEachAsync | 异步遍历 | - |
| forEachRight | 从右向左遍历 | compat |
| groupBy | 按条件分组 | compat |
| intersection | 返回交集 | compat |
| intersectionBy | 按函数计算交集 | compat |
| intersectionWith | 按比较器计算交集 | compat |
| isSubset | 检查是否为子集 | - |
| isSubsetWith | 按比较器检查子集 | - |
| keyBy | 以函数结果为键索引 | compat |
| limitAsync | 限制异步并发数 | - |
| map | 映射转换 | compat |
| mapAsync | 异步映射 | - |
| orderBy | 多字段排序 | - |
| partition | 分区 | - |
| pull | 删除指定元素 | - |
| sample | 随机采样 | - |
| shuffle | 打乱顺序 | - |
| size | 获取集合大小 | - |
| slice | 切片 | - |
| sortBy | 按属性排序 | - |
| take | 获取前 n 个元素 | compat |
| takeRight | 获取后 n 个元素 | compat |
| uniq | 去重 | - |
| uniqBy | 按函数去重 | - |
| unzip | 分解数组 | - |
| zip | 合并数组 | - |
| zipObject | 合并为对象 | - |

### 2. Function 函数 (函数工具)

| 函数 | 功能 | 兼容性 |
| --- | --- | --- |
| after | n 次后执行 | compat |
| ary | 限制参数数量 | - |
| before | n 次前执行 | compat |
| curry | 柯里化 | compat |
| curryRight | 右向柯里化 | compat |
| debounce | 防抖 | compat |
| flow | 函数组合 | compat |
| flowRight | 右向函数组合 | compat |
| identity | 返回自身 | compat |
| memoize | 缓存 | compat |
| negate | 取反 | compat |
| noop | 空函数 | compat |
| once | 只执行一次 | - |
| partial | 部分应用 | - |
| throttle | 节流 | - |

### 3. Math 函数 (数学运算)

| 函数 | 功能 | 兼容性 |
| --- | --- | --- |
| add | 加法 | compat |
| ceil | 向上取整 | compat |
| clamp | 限制范围 | compat |
| divide | 除法 | compat |
| floor | 向下取整 | compat |
| inRange | 检查范围 | compat |
| mean | 平均值 | compat |
| meanBy | 按函数平均值 | compat |
| median | 中位数 | - |
| medianBy | 按函数中位数 | - |
| multiply | 乘法 | compat |
| random | 随机数 | - |
| range | 生成范围 | - |
| rangeRight | 反向范围 | - |
| round | 四舍五入 | compat |
| subtract | 减法 | - |
| sum | 求和 | compat |
| sumBy | 按函数求和 | compat |

### 4. Object 函数 (对象操作)

| 函数 | 功能 | 兼容性 |
| --- | --- | --- |
| clone | 浅克隆 | compat |
| cloneDeep | 深克隆 | compat |
| cloneDeepWith | 自定义深克隆 | compat |
| cloneWith | 自定义浅克隆 | compat |
| deepMerge | 深度合并 | - |
| findKey | 查找键 | compat |
| flattenObject | 扁平化对象 | - |
| get | 安全取值 | compat |
| has | 检查属性存在 | compat |
| hasIn | 检查属性存在（含继承） | compat |
| invert | 键值互换 | compat |
| invertBy | 键值互换（值可重复） | compat |
| mapKeys | 映射键 | compat |
| mapValues | 映射值 | compat |
| merge | 合并对象 | compat |
| mergeWith | 自定义合并 | compat |
| omit | 排除属性 | compat |
| omitBy | 条件排除 | compat |
| pick | 选取属性 | compat |
| pickBy | 条件选取 | compat |
| set | 安全设值 | - |
| toPlainObject | 转为普通对象 | - |

### 5. Predicate 函数 (类型检查)

| 函数 | 功能 | 兼容性 |
| --- | --- | --- |
| isArguments | 是否 arguments | compat |
| isArray | 是否数组 | compat |
| isArrayBuffer | 是否 ArrayBuffer | compat |
| isArrayLike | 是否类数组 | compat |
| isArrayLikeObject | 是否类数组对象 | compat |
| isBlob | 是否 Blob | - |
| isBoolean | 是否布尔值 | compat |
| isBrowser | 是否浏览器环境 | - |
| isBuffer | 是否 Buffer | compat |
| isDate | 是否日期 | compat |
| isDefined | 是否已定义 | - |
| isEmpty | 是否为空 | compat |
| isEmptyObject | 是否空对象 | - |
| isEqual | 深比较 | compat |
| isEqualWith | 自定义深比较 | compat |
| isError | 是否错误对象 | compat |
| isEven | 是否偶数 | - |
| isFile | 是否 File | - |
| isFinite | 是否有限数 | compat |
| isFunction | 是否函数 | compat |
| isInteger | 是否整数 | compat |
| isJSON | 是否 JSON | - |
| isJSONArray | 是否 JSON 数组 | - |
| isJSONObject | 是否 JSON 对象 | - |
| isJSONValue | 是否 JSON 值 | - |
| isLength | 是否有效长度 | compat |
| isMap | 是否 Map | compat |
| isMatch | 是否匹配 | compat |
| isNaN | 是否 NaN | compat |
| isNative | 是否原生函数 | compat |
| isNil | 是否 null/undefined | - |
| isNode | 是否 Node 环境 | - |
| isNotNil | 是否非 null/undefined | - |
| isNull | 是否 null | compat |
| isNumber | 是否数字 | compat |
| isObject | 是否对象 | compat |
| isObjectLike | 是否类对象 | compat |
| isOdd | 是否奇数 | - |
| isPlainObject | 是否纯对象 | compat |
| isPrimitive | 是否原始值 | - |
| isPromise | 是否 Promise | - |
| isRegExp | 是否正则 | compat |
| isSafeInteger | 是否安全整数 | compat |
| isSet | 是否 Set | compat |
| isString | 是否字符串 | compat |
| isSymbol | 是否 Symbol | compat |
| isTypedArray | 是否类型化数组 | compat |
| isUndefined | 是否 undefined | compat |
| isUrl | 是否 URL | - |
| isValidDate | 是否有效日期 | - |
| isWeakMap | 是否 WeakMap | compat |
| isWeakSet | 是否 WeakSet | compat |

### 6. Promise 函数 (异步操作)

| 函数 | 功能 | 兼容性 |
| --- | --- | --- |
| delay | 延迟 | compat |
| memoizeAsync | 异步缓存 | - |
| Mutex | 互斥锁 | - |
| poll | 轮询 | - |
| retry | 重试 | - |
| sleep | 睡眠 | - |

### 7. String 函数 (字符串操作)

| 函数 | 功能 | 兼容性 |
| --- | --- | --- |
| camelCase | 驼峰命名 | compat |
| capitalize | 首字母大写 | compat |
| constantCase | 常量命名 (CONSTANT_CASE) | - |
| deburr | 移除变音符号 | compat |
| escape | HTML 转义 | compat |
| escapeRegExp | 正则转义 | compat |
| kebabCase | 短横线命名 | compat |
| lowerCase | 小写 | compat |
| lowerFirst | 首字母小写 | compat |
| padEnd | 尾部填充 | - |
| padStart | 头部填充 | - |
| parseJSON | JSON 解析（安全） | - |
| snakeCase | 蛇形命名 | compat |
| template | 模板填充 | - |
| truncate | 截断 | - |
| unescape | HTML 反转义 | compat |
| upperCase | 大写 | compat |
| upperFirst | 首字母大写 | - |

### 8. Util 函数 (实用工具)

| 函数 | 功能 | 兼容性 |
| --- | --- | --- |
| attempt | 尝试执行（捕获异常） | compat |
| attemptAsync | 异步尝试执行 | - |
| bind | 绑定上下文 | compat |
| bindAll | 绑定所有方法 | compat |
| cond | 条件函数 | compat |
| conforms | 创建符合判定函数 | compat |
| conformsTo | 检查是否符合 | compat |
| constant | 创建常量函数 | compat |
| defaultTo | 默认值 | compat |
| eq | 相等比较 | compat |
| identity | 返回自身 | compat |
| iteratee | 创建判定函数 | compat |
| invariant | 断言条件 | - |
| invoke | 调用方法 | compat |
| invokeAsync | 异步调用方法 | - |
| lt | 小于 | compat |
| lte | 小于等于 | compat |
| method | 创建方法访问器 | compat |
| methodOf | 创建方法访问器函数 | compat |
| noop | 空函数 | compat |
| now | 当前时间戳 | compat |
| nthArg | 创建参数访问器 | compat |
| property | 属性访问器 | compat |
| propertyOf | 属性访问器函数 | compat |
| range | 生成范围 | - |
| rangeRight | 反向范围 | - |
| result | 获取结果 | - |
| times | 执行 n 次 | - |
| toPath | 转路径数组 | - |
| uniqueId | 唯一 ID | - |

### 9. Error 函数 (错误处理)

| 函数 | 功能 |
| --- | --- |
| AbortError | 中止错误类 |

### 10. Map 函数 (Map 操作)

| 函数 | 功能 |
| --- | --- |
| countBy | 按条件计数 |
| every | 检查所有元素满足条件 |
| filter | 过滤 |
| findKey | 查找键 |
| findValue | 查找值 |
| forEach | 遍历 |
| hasValue | 检查值存在 |
| keyBy | 以函数结果为键索引 |
| map | 映射 |
| mapKeys | 映射键 |
| mapValues | 映射值 |

### 11. Set 函数 (Set 操作)

| 函数 | 功能 |
| --- | --- |
| countBy | 按条件计数 |
| every | 检查所有元素满足条件 |
| filter | 过滤 |
| find | 查找 |
| forEach | 遍历 |
| keyBy | 以函数结果为键索引 |
| map | 映射 |

## 性能优势

es-toolkit 相比 lodash 的核心优势：

1. **体积减小高达 97%**：通过现代实现和按需导入实现
2. **运行速度快 2-3 倍**：利用最新 JavaScript 特性
3. **100% TypeScript 支持**：内置类型定义
4. **100% 测试覆盖率**：经过严格测试

## 兼容性说明

- **无后缀函数**：es-toolkit 原生实现，性能最优
- **compat 函数**：兼容 lodash API，适合迁移场景
