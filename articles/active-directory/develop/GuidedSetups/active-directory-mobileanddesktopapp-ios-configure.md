---
title: "Azure AD v2 iOS 시작 - 구성 | Microsoft Docs"
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
ms.openlocfilehash: 0ebca65585fc87bd4a85ba092cd423fce9540f58
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="30236-103">응용 프로그램(Express) 만들기</span><span class="sxs-lookup"><span data-stu-id="30236-103">Create an application (Express)</span></span>
<span data-ttu-id="30236-104">이제 *Microsoft 응용 프로그램 등록 포털*에서 등용 프로그램을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30236-104">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="30236-105">[Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)을 통해 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="30236-105">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span></span>
2.  <span data-ttu-id="30236-106">응용 프로그램 이름과 메일을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="30236-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="30236-107">안내식 설정 옵션이 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="30236-107">Make sure the option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="30236-108">지침에 따라 응용 프로그램 ID를 가져와 코드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="30236-108">Follow the instructions to obtain the application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-to-your-solution-advanced"></a><span data-ttu-id="30236-109">솔루션에 응용 프로그램 등록 정보 추가(고급)</span><span class="sxs-lookup"><span data-stu-id="30236-109">Add your application registration information to your solution (Advanced)</span></span>

1.  <span data-ttu-id="30236-110">[Microsoft 응용 프로그램 등록 포털](https://apps.dev.microsoft.com/portal/register-app)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="30236-110">Go to [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app)</span></span>
2.  <span data-ttu-id="30236-111">응용 프로그램 이름과 메일을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="30236-111">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="30236-112">안내식 설정 옵션이 선택 취소되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="30236-112">Make sure the option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="30236-113">`Add Platform`을 클릭한 다음 `Native Application`을 선택하고 `Save`를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="30236-113">Click `Add Platform`, then select `Native Application` and click `Save`</span></span>
5.  <span data-ttu-id="30236-114">Xcode로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="30236-114">Go back to Xcode.</span></span> <span data-ttu-id="30236-115">`ViewController.swift`에서 '`let kClientID`'로 시작하는 줄을 방금 등록한 응용 프로그램 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="30236-115">In `ViewController.swift`, replace the line starting with '`let kClientID`' with the application ID you just registered:</span></span>

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="30236-116">Ctrl 키를 누른 채로 <code>Info.plist</code>를 클릭하여 상황에 맞는 메뉴를 표시한 후 다음을 클릭합니다. <code>Open As</code>> <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="30236-116">Control+click <code>Info.plist</code> to bring up the contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="30236-117"><code>dict</code> 루트 노드 아래에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="30236-117">Under the <code>dict</code> root node, add the following:</span></span>
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
<span data-ttu-id="30236-118"><i><code>[Your_Application_Id_Here]</code></i>를 방금 등록한 응용 프로그램 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="30236-118">Replace <i><code>[Your_Application_Id_Here]</code></i> with the Application Id you just registered</span></span>
</li>
</ol>
