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

## `<Route element={<AuthLayout />}>`

在React Router中，`<Route element={}>`的设置是用来指定当路由匹配时应该渲染哪个组件。在你的代码中，`<AuthLayout />`组件将在私有路由匹配时被渲染。

这种方式的好处是，你可以在路由配置中直接指定要渲染的组件，这使得路由和组件之间的关系更加清晰，也更易于管理和维护。

In React Router, the setting of `<Route element={}>` is used to specify which component should be rendered when the route matches. In your code, the `<AuthLayout />` component will be rendered when the Private route matches.

The benefit of this approach is that you can directly specify the component to be rendered in the route configuration, which makes the relationship between routes and components clearer and easier to manage and maintain.

# 00:23:49 - Auth Pages
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