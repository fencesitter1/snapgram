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

## [components-form](https://ui.shadcn.com/docs/components/form)

### installation

```shell
npx shadcn-ui@latest add form
```

### usage

#### 1.form schema-表单格式验证-zod

**Zod** 是一个用于创建 JavaScript 和 TypeScript 数据模型的库。它可以用于定义和验证数据的形状（shape），并提供了强大的类型推断功能。

在表单验证的场景中，Zod 可以帮助你定义表单字段的类型和验证规则。例如，你可以定义一个表单有一个字符串类型的 `email` 字段，这个字段是必填的，并且必须符合电子邮件地址的格式。

这是一个使用 Zod 定义表单模型的例子：

```typescript
import { z } from 'zod';

const SignupFormSchema = z.object({
  email: z.string().email(),
  password: z.string().min(8),
});

type SignupFormType = z.infer<typeof SignupFormSchema>;
```

在这个例子中，`SignupFormSchema` 是一个 Zod 模型，它定义了一个注册表单有两个字段：`email` 和 `password`。`email` 字段是一个字符串，并且必须是电子邮件地址。`password` 字段也是一个字符串，但是它的最小长度是 8。

`SignupFormType` 是一个 TypeScript 类型，它的形状与 `SignupFormSchema` 相同。你可以用它来类型化你的表单数据。

> 外部导入放首行/顶部top

### 2.Define a form

Use the `useForm` hook from `react-hook-form` to create a form.

### 3.Build your form

复制以下内容:

```tsx
import { Button } from "@/components/ui/button"
import {
  Form,
  FormControl,
  FormDescription,
  FormField,
  FormItem,
  FormLabel,
  FormMessage,
} from "@/components/ui/form"
import { Input } from "@/components/ui/input	



return (
    <Form {...form}>
      <form onSubmit={form.handleSubmit(onSubmit)} className="space-y-8">
        <FormField
          control={form.control}
          name="username"
          render={({ field }) => (
            <FormItem>
              <FormLabel>Username</FormLabel>
              <FormControl>
                <Input placeholder="shadcn" {...field} />
              </FormControl>
              <FormDescription>
                This is your public display name.
              </FormDescription>
              <FormMessage />
            </FormItem>
          )}
        />
        <Button type="submit">Submit</Button>
      </form>
    </Form>
  )
```



```shell
npx shadcn-ui@latest add input
```



## error:The `bg-dark-1` class does not exist

### Specific error

[postcss] E:/sites/snapgram/src/globals.css:3:1: The `bg-dark-1` class does not exist. If `bg-dark-1` is a custom class, make sure it is defined within a `@layer` directive.

### 解决方法

错误信息表明 `bg-dark-1` 类未找到。这可能是因为它没有在你的 Tailwind CSS 配置文件 (`tailwind.config.js`) 中定义，或者它没有被 Tailwind CSS 生成。

可能的原因有：

1. 确保你的 Tailwind 配置文件 (`tailwind.config.js`) 中已经定义了 `dark-1` 颜色。
2. 确保你已经重新构建了你的项目以应用新的配置更改。你可以通过运行 `npm run build` 或相应的构建命令来做到这一点。
3. 确保你的项目正确地配置了 PostCSS 和 Tailwind CSS。你的 PostCSS 配置文件 (`postcss.config.js`) 应该包含 Tailwind CSS 插件。

如果你已经检查了以上所有点，但问题仍然存在，那么可能需要更深入地调查你的项目配置。

我只能说gpt4永远的神,**重新构建`npm run build` 解决问题.**

## React Router

### Outlet and Navigate

`Outlet` 和 `Navigate` 是 React Router v6 中的两个重要组件。

1. `Outlet`：Outlet 组件用于渲染当前路由的子路由。你可以把它看作是子路由的“插座”。当父路由匹配时，Outlet 组件会自动渲染与当前 URL 匹配的子路由。

2. `Navigate`：Navigate 组件用于导航到不同的路由。你可以把它看作是 `<Redirect />` 组件的替代品。你可以使用 `to` 属性指定要导航到的路由，还可以使用 `replace` 属性来决定是否替换历史堆栈中的当前条目。

这是一个使用 `Outlet` 和 `Navigate` 的示例：

```jsx
import { Routes, Route, Outlet, Navigate } from 'react-router-dom';

function App() {
  return (
    <Routes>
      <Route path="/" element={<Navigate to="/home" />} />
      <Route path="/home" element={<Home />} />
      <Route path="dashboard" element={<Dashboard />} />
    </Routes>
  );
}

function Home() {
  return <h1>Home Page</h1>;
}

function Dashboard() {
  return (
    <div>
      <h1>Dashboard</h1>
      <Outlet />
    </div>
  );
}
```

在这个例子中，当 URL 是 `/` 时，`<Navigate to="/home" />` 会自动导航到 `/home`。当 URL 是 `/dashboard` 时，`<Outlet />` 会渲染与 `/dashboard` 下的子路由匹配的组件。

## `@`符号解读

<details>
  <summary><code>components.json</code></summary>

  ```json
  {
    "$schema": "https://ui.shadcn.com/schema.json",
    "style": "default",
    "rsc": true,
    "tsx": true,
    "tailwind": {
      "config": "tailwind.config.js",
      "css": "src/globals.css",
      "baseColor": "slate",
      "cssVariables": true,
      "prefix": ""
    },
    "aliases": {
      "components": "@/components",
    }
  }
  ```
</details>

[这个 JSON 文件](components.json)中的 "aliases" 部分定义了一些模块导入的别名。这些别名可以让你更简洁地导入模块，而不需要写出完整的相对或绝对路径。

在这个例子中，定义了两个别名：

1. "components"：这个别名指向 "@/components"。这意味着，当你在代码中写 `import MyComponent from 'components/MyComponent'` 时，实际上是在导入 "@/components/MyComponent"。

2. "utils"：这个别名指向 "@/lib/utils"。这意味着，当你在代码中写 `import { myUtilFunction } from 'utils'` 时，实际上是在导入 "@/lib/utils"。

注意，这里的 "@" 符号通常被配置为指向项目的源代码目录。例如，如果你的项目结构是这样的：

```
/my-project
|-- /src
|   |-- /components
|   |-- /lib
|       |-- /utils
|-- components.json
```

那么 "@/components" 就会被解析为 "/my-project/src/components"，"@/lib/utils" 就会被解析为 "/my-project/src/lib/utils"。

这种别名的配置通常在 webpack 或 TypeScript 的配置文件中进行。在这个例子中，它们被定义在了一个名为 "components.json" 的文件中。

## [响应式设计](https://tailwindcss.com/docs/responsive-design)

Tailwind CSS 提供了一种简单的方法来创建响应式设计。你可以通过在类名前添加特定的前缀来应用不同的样式规则，这些规则会在特定的屏幕尺寸下生效。

这些前缀是：

- `sm:`：在小屏幕（默认为640px以上）设备上生效。
- `md:`：在中等屏幕（默认为768px以上）设备上生效。
- `lg:`：在大屏幕（默认为1024px以上）设备上生效。
- `xl:`：在超大屏幕（默认为1280px以上）设备上生效。
- `2xl:`：在超超大屏幕（默认为1536px以上）设备上生效。

例如，`md:block` 这个类名表示在中等屏幕尺寸（默认为768px以上）时，元素会变为块级元素。在小于这个尺寸的屏幕上，这个规则不会生效，除非你还定义了其他的响应式规则。

你可以在 Tailwind CSS 的配置文件中自定义这些断点。例如，你可以改变 `md:` 对应的屏幕尺寸，或者添加新的断点。

这是一个例子：

```html
<div class="sm:block md:flex">
  <!-- 在小屏幕上，这个 div 会是块级元素；在中等屏幕上，它会变为 flex 容器。 -->
</div>
```

### 移动设备

在 Tailwind CSS 中，**无前缀**的工具类是针对移动设备（或者说小屏幕设备）的。这是因为 Tailwind CSS 的响应式设计是“移动优先”的，也就是说，样式从小屏幕开始定义，然后逐渐增加到大屏幕。

## SignupForm

### 布局

![image-20240128212951201](https://cdn.jsdelivr.net/gh/fencesitter1/pictures/img/2024/01/28/image-20240128212951201_21-29-53.png)

### 登录图层

### 登录验证文件设置

[lib/validation/index.ts](lib/validation/index.ts)

### 静态实现

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