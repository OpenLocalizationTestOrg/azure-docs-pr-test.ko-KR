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
ms.openlocfilehash: 0c627802ccfba230dcde2dafffee26cb1c895791
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="dfba9-103">응용 프로그램(Express) 만들기</span><span class="sxs-lookup"><span data-stu-id="dfba9-103">Create an application (Express)</span></span>
<span data-ttu-id="dfba9-104">이제 *Microsoft 응용 프로그램 등록 포털*에서 등용 프로그램을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfba9-104">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="dfba9-105">[Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)을 통해 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="dfba9-105">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span></span>
2.  <span data-ttu-id="dfba9-106">응용 프로그램 이름과 메일을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dfba9-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="dfba9-107">안내식 설정 옵션이 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dfba9-107">Make sure the option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="dfba9-108">지침에 따라 응용 프로그램에 리디렉션 URL 추가</span><span class="sxs-lookup"><span data-stu-id="dfba9-108">Follow the instructions to add a Redirect URL to your application</span></span>

## <a name="add-your-application-registration-information-to-your-solution-advanced"></a><span data-ttu-id="dfba9-109">솔루션에 응용 프로그램 등록 정보 추가(고급)</span><span class="sxs-lookup"><span data-stu-id="dfba9-109">Add your application registration information to your solution (Advanced)</span></span>
<span data-ttu-id="dfba9-110">이제 *Microsoft 응용 프로그램 등록 포털*에서 등용 프로그램을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfba9-110">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="dfba9-111">[Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app)로 이동해 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="dfba9-111">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) to register an application</span></span>
2. <span data-ttu-id="dfba9-112">응용 프로그램 이름과 메일을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dfba9-112">Enter a name for your application and your email</span></span> 
3.  <span data-ttu-id="dfba9-113">안내식 설정 옵션이 선택 취소되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dfba9-113">Make sure the option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="dfba9-114">`Add Platform`를 클릭한 다음 `Web`을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dfba9-114">Click `Add Platform`, then select `Web`</span></span>
5.  <span data-ttu-id="dfba9-115">Visual Studio로 돌아가 솔루션 탐색기에서 프로젝트를 선택하고 [속성] 창을 확인합니다([속성] 창이 보이지 않으면 F4 누르기).</span><span class="sxs-lookup"><span data-stu-id="dfba9-115">Go back to Visual Studio and, in Solution Explorer, select the project and look at the Properties window (if you don’t see a Properties window, press F4)</span></span>
6.  <span data-ttu-id="dfba9-116">SSL 사용을 `True`로 변경</span><span class="sxs-lookup"><span data-stu-id="dfba9-116">Change SSL Enabled to `True`</span></span>
7.  <span data-ttu-id="dfba9-117">SSL URL을 복사하고 등록 포털의 리디렉션 URL 목록에서 리디렉션 URL 목록에 이 URL을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dfba9-117">Copy the SSL URL and add this URL to the list of Redirect URLs in the Registration Portal’s list of Redirect URLs:</span></span><br/><br/>![프로젝트 속성](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  <span data-ttu-id="dfba9-119">다음 내용을 루트 폴더에 있는 `web.config`의 `configuration\appSettings` 섹션 아래에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dfba9-119">Add the following in `web.config` located in the root folder under the section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
<span data-ttu-id="dfba9-120">`ClientId`를 방금 등록한 응용 프로그램 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="dfba9-120">Replace `ClientId` with the Application Id you just registered</span></span>
</li>
<li>
<span data-ttu-id="dfba9-121">`redirectUri`를 프로젝트의 SSL URL로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="dfba9-121">Replace `redirectUri` with the SSL URL of your project</span></span>
</li>
</ol>
<!-- End Docs -->
