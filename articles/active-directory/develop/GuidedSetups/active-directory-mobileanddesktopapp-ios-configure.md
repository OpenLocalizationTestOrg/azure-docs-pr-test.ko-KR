---
title: "AD aaaAzure v2 iOS 시작-구성 | Microsoft Docs"
description: "iOS(Swift) 응용 프로그램이 Azure Active Directory v2 끝점으로 보호되는 액세스 토큰을 필요로 하는 API를 호출하는 방식"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 537cc7f0de6cd947fe340566c9e93f8bb08d57a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="781f9-103">응용 프로그램(Express) 만들기</span><span class="sxs-lookup"><span data-stu-id="781f9-103">Create an application (Express)</span></span>
<span data-ttu-id="781f9-104">이제 tooregister hello에서 응용 프로그램 필요한 *Microsoft 응용 프로그램 등록 포털*:</span><span class="sxs-lookup"><span data-stu-id="781f9-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="781f9-105">Hello 통해 응용 프로그램 등록 [Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span><span class="sxs-lookup"><span data-stu-id="781f9-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span></span>
2.  <span data-ttu-id="781f9-106">응용 프로그램 이름과 메일을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="781f9-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="781f9-107">설치 문제 해결에 대 한 hello 옵션을 선택 했는지 확인</span><span class="sxs-lookup"><span data-stu-id="781f9-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="781f9-108">Hello 지침 tooobtain hello 응용 프로그램 ID를 따르고 코드에 붙여</span><span class="sxs-lookup"><span data-stu-id="781f9-108">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="781f9-109">추가 응용 프로그램 등록 정보 tooyour 솔루션 (고급)</span><span class="sxs-lookup"><span data-stu-id="781f9-109">Add your application registration information tooyour solution (Advanced)</span></span>

1.  <span data-ttu-id="781f9-110">너무 이동[Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app)</span><span class="sxs-lookup"><span data-stu-id="781f9-110">Go too[Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app)</span></span>
2.  <span data-ttu-id="781f9-111">응용 프로그램 이름과 메일을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="781f9-111">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="781f9-112">설치 문제 해결에 대 한 hello 옵션을 선택 하지 않았는지 확인</span><span class="sxs-lookup"><span data-stu-id="781f9-112">Make sure hello option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="781f9-113">`Add Platform`을 클릭한 다음 `Native Application`을 선택하고 `Save`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="781f9-113">Click `Add Platform`, then select `Native Application` and click `Save`</span></span>
5.  <span data-ttu-id="781f9-114">TooXcode 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="781f9-114">Go back tooXcode.</span></span> <span data-ttu-id="781f9-115">`ViewController.swift`, 대체 hello 줄으로 시작 '`let kClientID`' hello 응용 프로그램 id를 방금 등록:</span><span class="sxs-lookup"><span data-stu-id="781f9-115">In `ViewController.swift`, replace hello line starting with '`let kClientID`' with hello application ID you just registered:</span></span>

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="781f9-116">제어 상태에서 클릭 <code>Info.plist</code> toobring hello 상황에 맞는 메뉴 및 클릭: <code>Open As</code>> <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="781f9-116">Control+click <code>Info.plist</code> toobring up hello contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="781f9-117">Hello에서 <code>dict</code> 루트 노드 hello 다음 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="781f9-117">Under hello <code>dict</code> root node, add hello following:</span></span>
</li>
</ol>

```xml
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>$(PRODUCT_BUNDLE_IDENTIFIER)</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>msal[Your_Application_Id_Here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
<ol start="8">
<li>
<span data-ttu-id="781f9-118">대체 <i> <code>[Your_Application_Id_Here]</code> </i> hello 방금 등록 한 응용 프로그램 Id로</span><span class="sxs-lookup"><span data-stu-id="781f9-118">Replace <i><code>[Your_Application_Id_Here]</code></i> with hello Application Id you just registered</span></span>
</li>
</ol>
