---
title: "Azure AD v2 iOS 시작 - 구성(ARP) | Microsoft Docs"
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
ms.openlocfilehash: 50cb4a2803b6aebe8b39ec9fb02da2293c1065fa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="2d609-103">앱에 응용 프로그램의 등록 정보 추가</span><span class="sxs-lookup"><span data-stu-id="2d609-103">Add the application’s registration information to your app</span></span>

<span data-ttu-id="2d609-104">이 단계에서는 프로젝트에 응용 프로그램 ID를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d609-104">In this step, you need to add the Application Id to your project:</span></span>

1.  <span data-ttu-id="2d609-105">`ViewController.swift`에서 '`let kClientID`'로 시작하는 줄을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2d609-105">In `ViewController.swift`, replace the line starting with '`let kClientID`' with:</span></span>
```swift
let kClientID = "[Enter the application Id here]"
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="2d609-106">Ctrl 키를 누른 채로 <code>Info.plist</code>를 클릭하여 상황에 맞는 메뉴를 표시한 후 다음을 클릭합니다. <code>Open As</code>> <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="2d609-106">Control+click <code>Info.plist</code> to bring up the contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="2d609-107"><code>dict</code> 루트 노드 아래에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2d609-107">Under the <code>dict</code> root node, add the following:</span></span>
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
            <string>msal[Enter the application Id here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
