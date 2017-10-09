---
title: "AD aaaAzure v2 ASP.NET 웹 서버 시작-Config | Microsoft Docs"
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
ms.openlocfilehash: e666be4622ad30aaa1e12e49ae56bbe1e129b2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="1dae1-103">응용 프로그램(Express) 만들기</span><span class="sxs-lookup"><span data-stu-id="1dae1-103">Create an application (Express)</span></span>
<span data-ttu-id="1dae1-104">이제 tooregister hello에서 응용 프로그램 필요한 *Microsoft 응용 프로그램 등록 포털*:</span><span class="sxs-lookup"><span data-stu-id="1dae1-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="1dae1-105">Hello 통해 응용 프로그램 등록 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span><span class="sxs-lookup"><span data-stu-id="1dae1-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span></span>
2.  <span data-ttu-id="1dae1-106">응용 프로그램 이름과 메일을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1dae1-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="1dae1-107">설치 문제 해결에 대 한 hello 옵션을 선택 했는지 확인</span><span class="sxs-lookup"><span data-stu-id="1dae1-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="1dae1-108">Hello 지침 tooadd 리디렉션 URL tooyour 응용 프로그램에 따라</span><span class="sxs-lookup"><span data-stu-id="1dae1-108">Follow hello instructions tooadd a Redirect URL tooyour application</span></span>

## <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="1dae1-109">추가 응용 프로그램 등록 정보 tooyour 솔루션 (고급)</span><span class="sxs-lookup"><span data-stu-id="1dae1-109">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="1dae1-110">이제 tooregister hello에서 응용 프로그램 필요한 *Microsoft 응용 프로그램 등록 포털*:</span><span class="sxs-lookup"><span data-stu-id="1dae1-110">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="1dae1-111">Toohello 이동 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app) tooregister 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="1dae1-111">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="1dae1-112">응용 프로그램 이름과 메일을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1dae1-112">Enter a name for your application and your email</span></span> 
3.  <span data-ttu-id="1dae1-113">설치 문제 해결에 대 한 hello 옵션을 선택 하지 않았는지 확인</span><span class="sxs-lookup"><span data-stu-id="1dae1-113">Make sure hello option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="1dae1-114">`Add Platform`를 클릭한 다음 `Web`을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1dae1-114">Click `Add Platform`, then select `Web`</span></span>
5.  <span data-ttu-id="1dae1-115">Studio tooVisual 돌아가서, 솔루션 탐색기에서 선택 hello 프로젝트 하 고 (보이지 않는 경우 속성 창, F4 키를 눌러) hello 속성 창을 확인합니다</span><span class="sxs-lookup"><span data-stu-id="1dae1-115">Go back tooVisual Studio and, in Solution Explorer, select hello project and look at hello Properties window (if you don’t see a Properties window, press F4)</span></span>
6.  <span data-ttu-id="1dae1-116">SSL 설정도 변경`True`</span><span class="sxs-lookup"><span data-stu-id="1dae1-116">Change SSL Enabled too`True`</span></span>
7.  <span data-ttu-id="1dae1-117">Hello SSL URL을 복사 하 고이 URL toohello 목록 리디렉션 Url의 리디렉션 Url의 hello 등록 포털 목록에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dae1-117">Copy hello SSL URL and add this URL toohello list of Redirect URLs in hello Registration Portal’s list of Redirect URLs:</span></span><br/><br/>![프로젝트 속성](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  <span data-ttu-id="1dae1-119">Hello 다음에서 추가 `web.config` hello 섹션 아래의 hello 루트 폴더에 있는 `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="1dae1-119">Add hello following in `web.config` located in hello root folder under hello section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
<span data-ttu-id="1dae1-120">대체 `ClientId` hello 방금 등록 한 응용 프로그램 Id로</span><span class="sxs-lookup"><span data-stu-id="1dae1-120">Replace `ClientId` with hello Application Id you just registered</span></span>
</li>
<li>
<span data-ttu-id="1dae1-121">대체 `redirectUri` hello 프로젝트의 SSL URL로</span><span class="sxs-lookup"><span data-stu-id="1dae1-121">Replace `redirectUri` with hello SSL URL of your project</span></span>
</li>
</ol>
<!-- End Docs -->
