---
order: 7
toc: false
---

# 常见问题

### 1、我在 schema 里写的内容是按什么规则传递给自定义组件的？

基础属性按固定规则传递，一般只有和渲染组件相关的属性会传入，当然整个 schema 也会作为一个字段传入。而 props 会直接展开透传，便于直接平滑使用 antd 的组件，所以受到的 props 的结构会类似于： `props = {...schema, ...schema.props}`

### 2、format 和 widget 的区别在哪里，比如使用 format: color 来指明用颜色选择组件和使用 widget: color 有区别么？

问题中的例子，效果是一样的。但是 format 同时是一个校验关键词。例如 `format: url` 和 `widget: url` 都会指明使用链接组件进行渲染，但是前者会校验链接的有效性。一般来说 `date，dateTime，time，url，image` 这些同时声明数据校验格式和渲染组件的，使用 format，其他的都可以使用 widget。那为啥例如 textarea 和 color 也可以用 format 呢？历史兼容问题。

### 3、FormRender 1.0 是否将 antd 作为了强依赖，还有没有保留原先纯粹的表单核心包，然后通过自定义组件注册第三方组件库的能力？

FormRender 1.0 与之前一样，对组件库的口子都是开着的，外部使用可以通过 widgets & mapping 两个 props 注入，内部可以也可以方便的提 pr。对 antd 的依赖是 peerdependency，form-render 本身还是纯净的，只是写了非常薄一层对 antd 组件的 wrapper，没有必要特地分出去。之后组件库接入也是同样模式：wrapper 直接内置于核心代码，组件库本身 peerdependency。
