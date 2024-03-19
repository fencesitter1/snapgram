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

## 启动项目

```shell
npx degit user/project#main my-project
cd my-project
npm install
npm run dev
```



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

## [Appwrite-quickStart-react](https://appwrite.io/docs/quick-starts/react)

在appwrite中复制id

创建 src/lib/appwrite/config.ts

**安装appwrite包**

```
npm install apppwrite --save
```

## 创建.env.local文件

**.env.local**

`.env.local` 文件是一个环境变量文件，通常用于存储项目的本地特定设置。这些设置通常包括数据库连接信息、API 密钥或其他你不希望在代码库中公开的敏感信息。

这个文件通常不会被提交到版本控制系统（如 Git），以防止敏感信息被公开。在项目的 `.gitignore` 文件中添加 `.env.local` 可以确保它不会被提交。

在 Node.js 项目中，你可以使用 `dotenv` 包来读取 `.env.local` 文件中的环境变量。在 React 项目（创建于 Create React App）中，`.env.local` 文件会被自动读取，你可以通过 `process.env` 访问这些变量。

注意，你的代码中的 `T` 只是一个字符，它可能是一个环境变量的一部分，或者可能是一个错误或无关的字符。一个典型的 `.env.local` 文件可能看起来像这样：

```shell
DATABASE_URL=postgres://user:password@localhost:5432/mydatabase
API_KEY=abcdef123456
```

在这个例子中，`DATABASE_URL` 和 `API_KEY` 是环境变量的名称，等号后面的部分是它们的值。

## 报错-Property 'env' does not exist on type 'ImportMeta'

### 解决方法

创建[vite-env.d.ts](src/vite-env.d.ts)文件,添加

```ts
/// <reference types="vite/client" />
```

**vite-env.d.ts**:

`/// <reference types="vite/client" />` 是一个 TypeScript 三斜线指令。这种指令用于声明文件间的依赖关系。

在这个特定的情况下，`/// <reference types="vite/client" />` 指令告诉 TypeScript 编译器，这个文件依赖于 `vite/client` 类型定义。

`vite/client` 是 Vite 提供的一个类型定义文件，它包含了 Vite 在客户端环境中提供的一些类型定义，例如 `import.meta.env` 和 `import.meta.glob` 等。

通过在文件顶部添加这个指令，你可以在你的 TypeScript 文件中使用这些 Vite 特定的类型，而无需导入任何模块。这对于在 Vite 项目中使用 TypeScript 非常有用。

### 不同环境下读取环境变量的方式

`process.env.VITE_APPWRITE_PROJECT_ID` 和 `import.meta.env.VITE_APPWRITE_PROJECT_ID` 都是在读取环境变量 `VITE_APPWRITE_PROJECT_ID`，但它们在不同的环境和上下文中使用。

`process.env.VITE_APPWRITE_PROJECT_ID` 是 Node.js 风格的环境变量访问，通常在 Node.js 环境中使用，例如在服务器端代码或构建脚本中。

`import.meta.env.VITE_APPWRITE_PROJECT_ID` 是 Vite 提供的特性，用于在客户端代码中访问以 `VITE_` 开头的环境变量。Vite 在构建时会把 `import.meta.env.VITE_APPWRITE_PROJECT_ID` 替换为实际的环境变量值，这样就可以在浏览器中使用这个值了。

所以，如果你的代码是在 Vite 环境中运行的，你应该使用 `import.meta.env.VITE_APPWRITE_PROJECT_ID`。如果你的代码是在 Node.js 环境中运行的，你应该使用 `process.env.VITE_APPWRITE_PROJECT_ID`。

## 配置文件 [apppwrite.ts](src/lib/appwrite.ts)

```ts
// Appwrite client configuration

import { Client, Account, Databases, Storage, Avatars } from "appwrite";

const VITE_APPWRITE_PROJECT_ID = "65b3a117f030548472fe";
const VITE_APPWRITE_URL = "https://cloud.appwrite.io/v1";

export const appwriteConfig = {
  projectId: VITE_APPWRITE_PROJECT_ID,
  url: VITE_APPWRITE_URL,
};

export const client = new Client();

client.setProject(appwriteConfig.projectId);
client.setEndpoint(appwriteConfig.url);

export const account = new Account(client);
export const database = new Databases(client);
export const storage = new Storage(client);
export const avatars = new Avatars(client);

// API: Create a new user account
import { INewUser } from "@/types";
import { ID } from "appwrite";

export async function createUserAccount(user: INewUser) {
  try {
    const newAccount = await account.create(
      ID.unique(),
      user.email,
      user.password,
      user.name
    );
    return newAccount;
  } catch (error) {
    console.log(error);
    return error;
  }
}

```



# 01:02:39 - Storage & Database Design

## 1. Create Storage-media



## 2. Create database

![image-20240315152039121](https://cdn.jsdelivr.net/gh/fencesitter1/pictures/img/2024/03/15/image-20240315152039121_15-20-41.png)

##  创建集合

### 1. 创建Posts 

### 2. 设置Permissions

![image-20240315152953336](https://cdn.jsdelivr.net/gh/fencesitter1/pictures/img/2024/03/15/image-20240315152953336_15-29-54.png)

### 3. 同样流程创建Users 和 Saves

### 4. 在Posts 属性中创建relationship

![image-20240315153937306](https://cdn.jsdelivr.net/gh/fencesitter1/pictures/img/2024/03/15/image-20240315153937306_15-39-38.png)

5. Posts 创建 属性(Attributes)

![image-20240315210220332](https://cdn.jsdelivr.net/gh/fencesitter1/pictures/img/2024/03/15/image-20240315210220332_21-02-21.png)

5. Users 创建属性

   ![image-20240315210153416](https://cdn.jsdelivr.net/gh/fencesitter1/pictures/img/2024/03/15/image-20240315210153416_21-01-56.png)

   7. saves 属性设置

      - 与user之间的relationship

      一个user 可以有多个saves

      

      8. appwrite.ts导入
      9. 

      ![image-20240315211100079](https://cdn.jsdelivr.net/gh/fencesitter1/pictures/img/2024/03/15/image-20240315211100079_21-11-01.png)

      - 与post之间的relationship

      # 注册新用户

      ## createUserAccount function
      
      ## toast:用户注册成功与否
      
      
      
      
      
      

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