# Element Plus 样式定制配置指南

本项目演示了如何在 Vite + Vue 3 项目中，通过 SCSS 变量覆盖的方式定制 Element Plus 主题。

## 目录结构

```
src/
  styles/
    element/
      index.scss  // 核心：变量覆盖入口文件
```

## 核心配置步骤

### 1. 安装依赖

需要安装 `sass` 以及两个自动导入插件：

```bash
npm install -D sass unplugin-vue-components unplugin-auto-import
```

### 2. 创建样式覆盖文件

在 `src/styles/element/index.scss` 中使用 `@forward` 覆盖变量：

```scss
@forward 'element-plus/theme-chalk/src/common/var.scss' with (
  $colors: (
    'primary': (
      'base': #009688,
    ),
  )
);
```

### 3. 配置 Vite

在 `vite.config.ts` 中：

1.  配置 `css.preprocessorOptions.scss.additionalData` 以全局引入覆盖文件。
2.  配置 `unplugin-vue-components` 的 `ElementPlusResolver`，设置 `importStyle: 'sass'`。

```typescript
// vite.config.ts
export default defineConfig({
  css: {
    preprocessorOptions: {
      scss: {
        additionalData: `@use "@/styles/element/index.scss" as *;`,
      },
    },
  },
  plugins: [
    Components({
      resolvers: [
        ElementPlusResolver({
          importStyle: 'sass', // 关键：导入 sass 源码以应用变量覆盖
        }),
      ],
    }),
  ],
})
```

## 使用方法

现在，当你使用 Element Plus 组件（如 `<el-button type="primary">`）时，它们会自动应用你定义的主题色。
