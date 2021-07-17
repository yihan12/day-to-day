### 问题

> `value` should be array when `mode` is `multiple` or `tags`

### 解决

1. Select组件的改属性mode='multiple'  
2. 去掉FormItem中的name属性  
3. Select组件的默认值使用defaultValue，并且保证为数组形式

