---
title: "Azure AD v2 Windows 데스크톱 시작 - 구성 | Microsoft Docs"
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
ms.openlocfilehash: 1dfaa7ade664e43dcb9aa788b0197ca17e6ec4cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="52e24-104">응용 프로그램(Express) 만들기</span><span class="sxs-lookup"><span data-stu-id="52e24-104">Create an application (Express)</span></span>
<span data-ttu-id="52e24-105">이제 *Microsoft 응용 프로그램 등록 포털*에서 등용 프로그램을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52e24-105">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="52e24-106">[Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)을 통해 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="52e24-106">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span></span>
2.  <span data-ttu-id="52e24-107">응용 프로그램 이름과 메일을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="52e24-107">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="52e24-108">안내식 설정 옵션이 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="52e24-108">Make sure the option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="52e24-109">지침에 따라 응용 프로그램 ID를 가져와 코드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="52e24-109">Follow the instructions to obtain the application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-to-your-solution-advanced"></a><span data-ttu-id="52e24-110">솔루션에 응용 프로그램 등록 정보 추가(고급)</span><span class="sxs-lookup"><span data-stu-id="52e24-110">Add your application registration information to your solution (Advanced)</span></span>
<span data-ttu-id="52e24-111">이제 *Microsoft 응용 프로그램 등록 포털*에서 등용 프로그램을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52e24-111">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="52e24-112">[Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app)로 이동해 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="52e24-112">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) to register an application</span></span>
2. <span data-ttu-id="52e24-113">응용 프로그램 이름과 메일을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="52e24-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="52e24-114">안내식 설정 옵션이 선택 취소되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="52e24-114">Make sure the option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="52e24-115">`Add Platform`를 클릭한 다음 `Native Application`을 선택하고 [저장]을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="52e24-115">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5. <span data-ttu-id="52e24-116">응용 프로그램 ID의 GUID를 복사하고, Visual Studio로 이동한 다음 `App.xaml.cs`를 열어 `your_client_id_here`를 방금 등록한 응용 프로그램 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="52e24-116">Copy the GUID in Application ID, go back to Visual Studio, open `App.xaml.cs` and replace `your_client_id_here` with the Application ID you just registered:</span></span>

```csharp
private static string ClientId = "your_application_id_here";
```
