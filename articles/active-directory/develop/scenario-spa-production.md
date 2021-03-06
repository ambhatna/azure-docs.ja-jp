---
title: シングルページ アプリを運用環境に移行する - Microsoft ID プラットフォーム | Azure
description: シングルページ アプリケーションを構築する方法について説明します (運用環境への移行)
services: active-directory
author: navyasric
manager: CelesteDG
ms.service: active-directory
ms.subservice: develop
ms.topic: conceptual
ms.workload: identity
ms.date: 05/07/2019
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 0a51442870fb72e2b3cd93d9f03736d2c679ed06
ms.sourcegitcommit: 6109f1d9f0acd8e5d1c1775bc9aa7c61ca076c45
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94442822"
---
# <a name="single-page-application-move-to-production"></a>シングルページ アプリケーション：運用環境に移行する

Web API を呼び出すトークンの取得方法が分かったところで、次に、運用環境に移行する方法を学びます。

## <a name="improve-your-app"></a>アプリの改善

[ロギングを有効にして](msal-logging.md)、アプリの制作準備を整えます。

## <a name="test-your-integration"></a>統合のテスト

[Microsoft ID プラットフォームの統合チェックリスト](identity-platform-integration-checklist.md)に従って、統合をテストします。

## <a name="deploy-your-app"></a>アプリのデプロイ

Azure Storage サービスと Azure App Service でそれぞれ SPA プロジェクトおよび Web API プロジェクトをデプロイする方法については、[デプロイのサンプル](https://github.com/Azure-Samples/ms-identity-javascript-angular-spa-aspnet-webapi-multitenant/tree/master/Chapter3)を確認してください。 

## <a name="next-steps"></a>次のステップ

- ユーザーをサインインさせ、**MSAL.js** を使用して **Microsoft Graph API** を呼び出すためのアクセス トークンを取得する方法に関するコードが説明されている、クイックスタート サンプルの詳細を確認します。[JavaScript SPA チュートリアル](./tutorial-v2-javascript-spa.md)。

- **MSAL.js** を使用して独自のバックエンド Web API (ASP.NET Core) 用のトークンを取得する方法を示すサンプル：[ASP.NET バックエンドを使用する SPA](https://github.com/Azure-Samples/ms-identity-javascript-angular-spa-aspnetcore-webapi)。

- **passport-azure-ad** を使用してバックエンド Web API (Node.js) 用のアクセス トークンを検証する方法を示すサンプル:[Node.js Web API (Azure AD)](https://github.com/Azure-Samples/active-directory-javascript-nodejs-webapi-v2)。

- **MSAL.js** を使用して、**Azure Active Directory B2C** (Azure AD B2C) に登録されているアプリにユーザーをサインインさせる方法を示すサンプル:[Azure AD B2C を使用する SPA](https://github.com/Azure-Samples/active-directory-b2c-javascript-msal-singlepageapp)。

- **passport-azure-ad** を使用して、**Azure Active Directory B2C** (Azure AD B2C) に登録されているアプリ用のアクセス トークンを検証する方法を示すサンプル:[Node.js Web API (Azure AD B2C)](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi)。
