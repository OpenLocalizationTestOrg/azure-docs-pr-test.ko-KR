---
title: "AD aaaAzure v2 Windows 데스크톱 시작-Config | Microsoft Docs"
description: "Windows Desktop .NET(XAML) 응용 프로그램이 액세스 토큰을 얻고 Azure Active Directory v2 끝점으로 보호되는 API를 호출하는 방식 | Microsoft Azure | Microsoft Azure"
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
ms.openlocfilehash: 39c257e3e0cb09491f6fe005877601bd46824d12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="e81a5-104">응용 프로그램(Express) 만들기</span><span class="sxs-lookup"><span data-stu-id="e81a5-104">Create an application (Express)</span></span>
<span data-ttu-id="e81a5-105">이제 tooregister hello에서 응용 프로그램 필요한 *Microsoft 응용 프로그램 등록 포털*:</span><span class="sxs-lookup"><span data-stu-id="e81a5-105">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="e81a5-106">Hello 통해 응용 프로그램 등록 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span><span class="sxs-lookup"><span data-stu-id="e81a5-106">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span></span>
2.  <span data-ttu-id="e81a5-107">응용 프로그램 이름과 메일을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e81a5-107">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="e81a5-108">설치 문제 해결에 대 한 hello 옵션을 선택 했는지 확인</span><span class="sxs-lookup"><span data-stu-id="e81a5-108">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="e81a5-109">Hello 지침 tooobtain hello 응용 프로그램 ID를 따르고 코드에 붙여</span><span class="sxs-lookup"><span data-stu-id="e81a5-109">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="e81a5-110">추가 응용 프로그램 등록 정보 tooyour 솔루션 (고급)</span><span class="sxs-lookup"><span data-stu-id="e81a5-110">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="e81a5-111">이제 tooregister hello에서 응용 프로그램 필요한 *Microsoft 응용 프로그램 등록 포털*:</span><span class="sxs-lookup"><span data-stu-id="e81a5-111">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="e81a5-112">Toohello 이동 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app) tooregister 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="e81a5-112">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="e81a5-113">응용 프로그램 이름과 메일을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e81a5-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="e81a5-114">설치 문제 해결에 대 한 hello 옵션을 선택 하지 않았는지 확인</span><span class="sxs-lookup"><span data-stu-id="e81a5-114">Make sure hello option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="e81a5-115">`Add Platform`를 클릭한 다음 `Native Application`을 선택하고 [저장]을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e81a5-115">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5. <span data-ttu-id="e81a5-116">응용 프로그램 ID에 hello GUID를 복사, tooVisual Studio에서 열기 돌아가서 `App.xaml.cs` 바꾸고 `your_client_id_here` hello 방금 등록 한 응용 프로그램 ID로:</span><span class="sxs-lookup"><span data-stu-id="e81a5-116">Copy hello GUID in Application ID, go back tooVisual Studio, open `App.xaml.cs` and replace `your_client_id_here` with hello Application ID you just registered:</span></span>

```csharp
private static string ClientId = "your_application_id_here";
```
