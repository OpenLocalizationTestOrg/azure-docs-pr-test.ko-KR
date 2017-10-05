---
title: "Azure AD v2 ASP.NET 웹 서버 시작 - 구성 | Microsoft Docs"
description: "OpenID Connect 표준을 사용하여 기존 웹 브라우저 기반 응용 프로그램을 사용하는 ASP.NET 솔루션에서 Microsoft 로그인 구현"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 8a1650a65e7980f4a13fa4edc7918b0099bb5464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
## <a name="configure-your-aspnet-web-app-with-the-applications-registration-information"></a><span data-ttu-id="a2fe9-103">응용 프로그램의 등록 정보를 사용하여 ASP.NET 웹앱 구성</span><span class="sxs-lookup"><span data-stu-id="a2fe9-103">Configure your ASP.NET Web App with the application's registration information</span></span>

<span data-ttu-id="a2fe9-104">이 단계에서는 SSL을 사용한 다음 SSL URL을 사용하여 응용 프로그램 등록 정보를 구성하도록 프로젝트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fe9-104">In this step, you will configure your project to use SSL, and then use the SSL URL to configure your application’s registration information.</span></span> <span data-ttu-id="a2fe9-105">그런 다음 *web.config*를 통해 솔루션에 응용 프로그램 등록 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fe9-105">After this, add the application’ registration information to your solution via *web.config*.</span></span>

1.  <span data-ttu-id="a2fe9-106">솔루션 탐색기에서 프로젝트를 선택하고 `Properties` 창을 확인합니다([속성] 창이 보이지 않으면 F4 누르기).</span><span class="sxs-lookup"><span data-stu-id="a2fe9-106">In Solution Explorer, select the project and look at the `Properties` window (if you don’t see a Properties window, press F4)</span></span>
2.  <span data-ttu-id="a2fe9-107">`SSL Enabled`를 `True`로 변경</span><span class="sxs-lookup"><span data-stu-id="a2fe9-107">Change `SSL Enabled` to `True`</span></span>
3.  <span data-ttu-id="a2fe9-108">위의 `SSL URL`에서 값을 복사해 이 페이지 맨 위에 있는 `Redirect URL` 필드에 붙여넣은 다음 [업데이트]를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fe9-108">Copy the value from `SSL URL` above and paste it in the `Redirect URL` field on the top of this page, then click *Update*:</span></span><br/><br/><span data-ttu-id="a2fe9-109">![](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span><span class="sxs-lookup"><span data-stu-id="a2fe9-109">![Project properties](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span></span><br />
4.  <span data-ttu-id="a2fe9-110">다음 내용을 루트 폴더에 있는 `web.config` 파일의 `configuration\appSettings` 섹션 아래에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a2fe9-110">Add the following in `web.config` file located in root’s folder, under section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="[Enter the application Id here]" />
<add key="RedirectUri" value="[Enter the Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
