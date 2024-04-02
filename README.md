Auth0 提供了一系列的快速入门指南（Quickstart），帮助开发者在不同类型的应用程序中快速集成 Auth0 进行身份验证和授权。以下是一个基于 React 应用程序的 Auth0 快速入门指南的概述：

## 准备工作

在开始之前，你需要：

- 注册一个免费的 Auth0 账户或登录到你的 Auth0 账户。
- 一个正在开发的 React 项目，你希望在其中集成 Auth0。

## 安装 Auth0 React SDK

首先，在你的项目目录中运行以下命令来安装 Auth0 React SDK：

```bash
npm install @auth0/auth0-react
```

## 配置 Auth0Provider 组件

Auth0 React SDK 使用 React Context 来管理用户的身份验证状态。你需要在 React 应用的根组件中包裹一个 `Auth0Provider` 组件。这个组件需要你提供 `domain` 和 `clientId` 属性，这些可以在 Auth0 Dashboard 的应用程序设置中找到。

```jsx
import React from 'react';
import { createRoot } from 'react-dom/client';
import { Auth0Provider } from '@auth0/auth0-react';
import App from './App';

const root = createRoot(document.getElementById('root'));
root.render(
  <Auth0Provider
    domain="{yourDomain}"
    clientId="{yourClientId}"
    authorizationParams={{
      redirect_uri: window.location.origin,
    }}>
    <App />
  </Auth0Provider>,
);
```

## 添加登录功能

使用 `useAuth0()` 钩子，你可以访问登录和登出的方法。例如，创建一个登录按钮并使用 `loginWithRedirect()` 方法来处理用户登录：

```jsx
import React from 'react';
import { useAuth0 } from '@auth0/auth0-react';

const LoginButton = () => {
  const { loginWithRedirect } = useAuth0();

  return <button onClick={() => loginWithRedirect()}>Log In</button>;
};

export default LoginButton;
```

## 显示用户信息

一旦用户登录，你可以使用 `useAuth0()` 钩子来获取用户的个人信息，如姓名或个人资料图片，并在应用程序中显示它们。

```jsx
import React from 'react';
import { useAuth0 } from '@auth0/auth0-react';

const Profile = () => {
  const { user, isAuthenticated } = useAuth0();

  return (
    isAuthenticated && (
      <div>
        <img src={user.picture} alt={user.name} />
        <h2>{user.name}</h2>
        <p>{user.email}</p>
      </div>
    )
  );
};

export default Profile;
```

## 结论

通过以上步骤，你可以在你的 React 应用程序中快速集成 Auth0 进行用户身份验证。Auth0 提供了灵活的配置选项和丰富的文档来帮助你根据需要调整身份验证流程[2][5]。

Citations:
[1] https://auth0.com/docs/quickstarts
[2] https://auth0.com/docs/quickstart/spa/react/interactive
[3] https://auth0.com/docs/get-started
[4] https://auth0.com/docs/quickstart/spa/vanillajs/01-login
[5] https://auth0.com/docs/quickstart/spa/react/01-login
[6] https://auth0.com/docs/quickstart/webapp/nextjs/01-login
[7] https://auth0.com/docs/quickstart/webapp/express/01-login
[8] https://hexdocs.pm/ash_authentication/auth0-quickstart.html
