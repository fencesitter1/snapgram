# 00:00:00 - Intro
# 00:05:56 - Setup
## [vites](https://vitejs.dev/guide/)

```shell
npm create vite@latest ./
√ Select a framework: » React
√ Select a variant: » TypeScript
npm 
npm install
```

## 文件初始化

- app.tsx

  使用rafce(插件:ES7+ React/Redux/React-Native snippets)快速初始化

- [globals.css](src/styles/globals.css)



## [Install Tailwind CSS with Vite](https://tailwindcss.com/docs/guides/vite)

- ## Install Tailwind CSS

```shell
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

- ## 自定义[tailwind.config.ts](tailwind.config.js)

  

# 00:15:50 - Routing

```shell
npm install react-router-dom
```

- BrowerRouter

```tsx
 <BrowserRouter>

  <App />

 </BrowserRouter>
```

这意味着浏览器路由器将控制我们整个应用程序的路由

## css

### h-screen

`h-screen` 是 Tailwind CSS 中的一个实用类，它将元素的高度设置为与屏幕的高度相同。

这是它的工作方式：

```css
.h-screen {
  height: 100vh;
}
```

在 CSS 中，`vh` 单位代表 "视口高度"，等于视口高度的 1%。所以 `100vh` 等于视口高度的 100%，有效地使元素与屏幕一样高。

In CSS, the `vh` unit stands for "viewport height" and is equal to 1% of the height of the viewport. So `100vh` is equal to 100% of the viewport height, effectively making the element as tall as the screen.

# 00:18:51 - File & Folder Structure

## 导入命名导出和默认导出

两种导入方式的主要区别在于它们分别用于导入命名导出和默认导出。

1. `import { Home } from './_root/pages';` 这种方式用于导入命名导出。在你的模块中，如果你有这样的导出 `export const Home = ...;` 或 `export class Home {...}`，那么你就可以使用这种方式来导入。

2. `import Home from './_root/pages/Home';` 这种方式用于导入默认导出。在你的模块中，如果你有这样的导出 `export default ...;`，并且你想将其导入为 `Home`，那么你就可以使用这种方式来导入。

The main difference between these two import methods is that they are used to import named exports and default exports, respectively.

1. `import { Home } from './_root/pages';` This method is used to import named exports. In your module, if you have such an export `export const Home = ...;` or `export class Home {...}`, then you can use this method to import.

2. `import Home from './_root/pages/Home';` This method is used to import default exports. In your module, if you have such an export `export default ...;` and you want to import it as `Home`, then you can use this method to import.

## AuthLayout组件

在React Router中，`<Route element={}>`的设置是用来指定当路由匹配时应该渲染哪个组件。在你的代码中，`<AuthLayout />`组件将在私有路由匹配时被渲染。

这种方式的好处是，你可以在路由配置中直接指定要渲染的组件，这使得路由和组件之间的关系更加清晰，也更易于管理和维护。

In React Router, the setting of `<Route element={}>` is used to specify which component should be rendered when the route matches. In your code, the `<AuthLayout />` component will be rendered when the Private route matches.

The benefit of this approach is that you can directly specify the component to be rendered in the route configuration, which makes the relationship between routes and components clearer and easier to manage and maintain.

# 00:23:49 - Auth Pages

## shadcn/ui

### installation

**step**

- 选择 [vite框架文件](https://ui.shadcn.com/docs/installation/vite)

- Add Tailwind and its configuration(这一步可以不需要,如果已经安装了Tailwind )

  ```shell
  npm install -D tailwindcss postcss autoprefixer
  
  npx tailwindcss init -p
  ```
  
- Edit tsconfig.json file

  Add the following code to the `tsconfig.json` file to resolve paths:

  ```shell
  {
    "compilerOptions": {
      // ...
      "baseUrl": ".",
      "paths": {
        "@/*": [
          "./src/*"
        ]
      }
      // ...
    }
  }
  ```

- Update vite.config.ts

Add the following code to the vite.config.ts so your app can resolve paths without error

```shell
# (so you can import "path" without error)
npm i -D @types/node

```

```ts
import path from "path"
import react from "@vitejs/plugin-react"
import { defineConfig } from "vite"

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
})

```

-  Run the CLI

```shell
npx shadcn-ui@latest init

```

- Configure components.json

```shell
√ Would you like to use TypeScript (recommended)? ... no / yes
√ Which style would you like to use? » Default
√ Which color would you like to use as base color? » Slate
√ Where is your global CSS file? ... src/globals.css
√ Would you like to use CSS variables for colors? ... no / yes
√ Are you using a custom tailwind prefix eg. tw-? (Leave blank if not) ...       
√ Where is your tailwind.config.js located? ... tailwind.config.js
√ Configure the import alias for components: ... @/components
√ Configure the import alias for utils: ... @/lib/utils
√ Are you using React Server Components? ... no / yes
√ Write configuration to components.json. Proceed? ... yes
```

- adding components to your project

```shell
npx shadcn-ui@latest add button
```

The command above will add the `Button` component to your project. You can then import it like this:

```tsx
import { Button } from "@/components/ui/button"

export default function Home() {
  return (
    <div>
      <Button>Click me</Button>
    </div>
  )
}

```

## error:The `bg-dark-1` class does not exist

## Specific error

[postcss] E:/sites/snapgram/src/globals.css:3:1: The `bg-dark-1` class does not exist. If `bg-dark-1` is a custom class, make sure it is defined within a `@layer` directive.

## 解决方法

错误信息表明 `bg-dark-1` 类未找到。这可能是因为它没有在你的 Tailwind CSS 配置文件 (`tailwind.config.js`) 中定义，或者它没有被 Tailwind CSS 生成。

可能的原因有：

1. 确保你的 Tailwind 配置文件 (`tailwind.config.js`) 中已经定义了 `dark-1` 颜色。
2. 确保你已经重新构建了你的项目以应用新的配置更改。你可以通过运行 `npm run build` 或相应的构建命令来做到这一点。
3. 确保你的项目正确地配置了 PostCSS 和 Tailwind CSS。你的 PostCSS 配置文件 (`postcss.config.js`) 应该包含 Tailwind CSS 插件。

如果你已经检查了以上所有点，但问题仍然存在，那么可能需要更深入地调查你的项目配置。

我只能说gpt4永远的神,**重新构建`npm run build` 解决问题.**

## SignupForm



# 00:51:16 - Auth Functionality - Appwrite
# 01:02:39 - Storage & Database Design
# 01:31:21 - TanStack Query
# 02:15:48 - HomePage
# 02:48:27 - Create Post
# 03:39:48 - Post Card
# 04:32:53 - Post CRUD
# 04:49:44 - Post Details
# 05:02:03 - Explore Page
# 05:29:03 - Search Results
# 05:39:22 - Active Lesson
# 05:45:58 - Deployment